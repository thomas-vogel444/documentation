# Unit Testing Controllers

See https://www.playframework.com/documentation/2.6.x/ScalaTestingWithScalaTest

## Dependency

Use the `scalatestplus` library at `"org.scalatestplus.play" %% "scalatestplus-play" % "x.x.x" % "test"`.

Use the version that matches your Play version. Check the [release compatibitily matrix][https://github.com/playframework/scalatestplus-play#releases].

## Imports

```scala
import org.scalatestplus.play._
import org.scalatestplus.play.guice._
import play.api.test._
import play.api.test.Helpers._
```

## Usage

Define test classes by extending the `PlaySpec` trait.

Create requests using `FakeRequest`.

Useful components are located in the `play.api.test.Helpers` class.
- RouteInvokers for testing routes
- ResultExtractors for extracting values from the Result
- StubControllerComponentsFactory for providing minimal controller components to the Controller to test.
- FutureAwaits + DefaultAwaitTimeout