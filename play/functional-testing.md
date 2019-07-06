# Functional tests of Play 2.6 Apps 

See https://www.playframework.com/documentation/2.6.x/ScalaFunctionalTestingWithScalaTest

Play applications are created using a `GuiceApplicationBuilder`. 
If you are testing the test the real HTTP stack, mix in `GuiceOneServerPerSuite` or ``GuiceOneServerPerTest``, both of which also provide a `fakeApplication`. 

You can configure the tests to use one server for multiple test classes.

Get the `fakeApplication` components using the `injector.instanceOf` method.

```scala
application.injector.instanceOf[WSClient]
```

## Useful trait to mix in

- PlaySpec
- GuiceOneAppPerSuite