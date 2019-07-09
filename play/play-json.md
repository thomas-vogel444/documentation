# Play Json

From https://www.playframework.com/documentation/2.6.x/ScalaJson

## Features

- Automatic conversion to and from case classes.
- Custom validation while parsing
- Automatic parsing in request bodiesl with auto-generated errors if content isn't parseable or incorrect Content-tyope headers are supplied.
- Can be used as a standalone library via `libraryDependencies += "com.typesafe.play" %% "play-json" % playVersion`

## Domain

Play json provides 3 types:
- JsValue: a trait representing any Json value.
    - JsString
    - JsNumber
    - JsBoolean
    - JsArray
    - JsObject
    - JsNull
- Json: utility object for json conversion
- JsPath: a path into JsValue

## Converting to a JsValue

### Using string parsing

```scala
val json: JsValue = Json.parse("""{"name": "Thomas","age": 32, "hobbies": ["dancing", "cycling"]}""")
```

### Using class construction

```scala
import play.api.libs.json._

val json: JsValue = Json.obj("name" -> "Thomas", "age": 32, "hobbies": Json.arr("dancing", "cycling"))
```

### Using Writes converters

Give `case class Person(name: String, age: Int)`

```scala
implicit val personWrite = new Writes[Person] {
    def writes(person: Person) = Json.obj(
        "name" -> person.name,
        "age" -> person.age
    )
}
```

### Traversing a JsValue structure

Given the above json defined

- Simple path 
```scala
val name = (json \ "name").get
```

- Recursive path
```scala
val names = json \\ "name"
```

- Direct lookup using the apply method on the json object itself
```scala
val name = json("name")
```

## Converting from a JsValue

### Using String utilities

```scala 
val minifiedString: String = Json.stringify(json)
val readableString: String = Json.prettyPrint(json)
```

### Using JsValue.as/asOpt

```scala
val name = (json \ "name").as[String]
val nameOption = (json \ "name").asOpt[String]
```

### Using validation (preferred way)

Does validation and returns a `JsResult` which has 2 classes:
- `JsSuccess`
- `JsError`

```scala
val nameResult = JsResult[String] = (json \ "name").validate[String]
```

