# Official Scala Driver

There is 

## Background

### Observable API

From http://mongodb.github.io/mongo-scala-driver/2.6/getting-started/quick-tour-primer/

The Scala API makes use of a custom implementation of the Observer pattern with 3 traits:
- Observable
    - subscribe
- Observer
    - onSubscribe
    - onNext
    - onError
    - onComplete
- Subscription
    - request

## Quick Tour

From http://mongodb.github.io/mongo-scala-driver/2.6/getting-started/quick-tour/

### Connect to Mongo

```scala
val mongoClient: MongoClient = MongoClient()
val database: MongoDatabase = mongoClient.getDatabase("mydb")
val collection = db.getCollection("myCollection")
```

### Insert documents

```scala
val document = Document("name" -> "Thomas", "age" -> 32)
collection.insertOne(document).toFuture()
collection.insertMany(...).toFuture()
```

### Query the collection

```scala
import org.mongodb.scala.model.Filters._
collection.find(equal("name", "Thomas"))
```