# Routing

## Binding Custom Types 

### For Path Parameters

Given 
```scala 
case class User(id: Int, name: String)
```

Define a `PathBindable[A]` for `User` given a `:id` path parameter
```scala
implicit def pathBinder(implicitBinder: PathBindable[Int]) = new PathBindable[User] {
    override def bind(key: String, value: String): Either[String, User] = {
        for {
            id   <- intBinder.bind(key, value).right
            user <- User.findById(id).toRight("User not found").right
        } yield user
    }
    override def unbind(key: String, user: User): String = {
        user.id.toString
    }
}
```

On the Controller side
```scala 
def user(user: User) = Action {
    Ok(user.name)
}
```

On the routes configuration file
```
GET  /user/:user  controllers.user(user: path.to.User)
```

### For Query Parameters

Use the `QueryStringBindable[A]` which is similar to PathBindable.