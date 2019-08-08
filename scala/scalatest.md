# Scalatest

## Cheatsheet

```scala
List() shouldBe empty

Future.failed(new Exception("Error!")).failed.futureValue shouldBe a [Upstream5xxResponse]
```