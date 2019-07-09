# Action Composition

Implement the `ActionBuilder` trait. 

## Questions

- What is the difference between ActionBuilder and ActionBuilderImpl?

## First way: override the `invokeBlock` method

```scala
import play.api.mvc._

class LoggingAction @Inject()(parser: BodyParsers.Default)(implicit ec: ExecutionContext) extends ActionBuilderImpl(parser) {
  override def invokeBlock[A](request: Request[A], block: (Request[A]) => Future[Result]) = {
    Logger.info("Calling action")
    block(request)
  }
}
```

Use dependency injection to get the action in the Controller. 

## Composing actions

If your action code is to be reused, implement it by wrapping the actions:

```scala
import play.api.mvc._

case class Logging[A](action: Action[A]) extends Action[A] {
    def apply(request: Request[A]): Future[Result] = {
        Logger.info("whatever...")
        action(request)
    }

    override def parser = action.parser
    override def executionContext = action.executionContext
}
```

Or

```scala 
import play.api.mvc._

def logging[A](action: Action[A]) = Action.async(action.parser) { request =>
    Logger.info("Whatever...")
    action(request)
}
```

Use it by wrapping the `Action`

```scala
def index = 
    Logging {
        Action {
            Ok
        }
    }
```

## Actions impacting the request

## Different request types

Use `ActionFunctions` for creating pipelines of data transformations or perform validation on the request.

Pre-defined traits implementing `ActionFunction`:
- `ActionTransformer`: can change the request 
- `ActionFilter`: can selectively intercept the request
- `ActionRefiner`: general case for both the above
- `ActionBuilder`: special case of functions that take Request as input

## Adding fields to a Request

Wrap the request with a class extending `WrappedRequest[A](request)`

E.g. for adding a username to the request:
```scala
class UserRequest[A](val username: Option[String], request: Request[A]) extends WrappedRequest[A](request)

class UserAction @Inject()(val parser BodyParsers.Default)(implicit val executionContext: ExecutionContext) 
    extends ActionBuilder[UserRequest, AnyContent]
    with ActionTransformer[Request, UserRequest] {

        def transform[A](request: Request[A]) = 
            Future.successful {
                new UserRequest(request.session.get("username"), request)
            }
    }
```

Another

```scala
class ItemRequest[A](val item: Item, request: UserRequest[A]) extends WrappedRequest[A](request) {
    def username = request.username
}

def ItemAction(itemId: String)(implicit ex: ExecutionContext) = new ActionRefiner[UserRequest, ItemRequest] {
    def executionContext = ec

    def refine[A](input: UserRequest[A]) = 
        Future.successful {
            ItemDao
                .findItemById(itemId)
                .map(new ItemRequest(_, input))
                .toRight(NotFound)
        }
}

```

## Putting it all together

Chain actions together using the `andThen` to create an action:

```scala
def tagItem(itemId: String, tag: String)(implicit ec: ExecutionContext) = 
    userAction.andThen(ItemAction(itemId)).andThen(PermissionCheckAction) { request =>
        request.item.addTag(tag)
        Ok("User " + request.username + " tagged " + request.item.id)
    }
```