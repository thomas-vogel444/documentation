# BodyParsers

## Existing ones

Play provides a number of predifined BodyParsers available in the trait `PlayBodyParsers` which is available in the controller through the `parser` argument.

## Modifying existing ones

You can make your own from existing `BodyParsers`. Use the methods 
- `map` || `mapM`
- `validate` || `validateM`

```scala
val updateBodyParser = 
    parse.text.validate {
      case "shuttered" => Right(Shuttered)
      case "unshuttered" => Right(UnShuttered)
      case _ => Left(BadRequest("Body should contain either 'shuttered' or 'unshuttered'"))
    }
```

## Custom BodyParsers

Entirely custom BodyParsers can be made by extending the `BodyParser` trait.

```scala
case class Person(name: Stringl, age: Int)

class MyBodyParser extends BodyParser[Person] {
    override def apply(v1: RequestHeader): Accumulator[ByteString, Either[Result, Person]] = ???
}
```

The `Accumulator` is a wrapper around an Akka Stream source. Use the Akka Stream library to modify it in any way you see fit.