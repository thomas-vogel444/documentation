# Testing with Mockito

Introduce it in the test via the `MockitoSugar` trait
```scala
import org.mockito.scalatest.MockitoSugar

class MySpec extends WordSpec with MockitoSugar {
    ...
}
```

## Setting up conditions

Some examples:

```scala
val myService = mock[MyService]

when(myService.someMethod(someArgument)).thenReturn(Future.successfull("Some result..."))

when(myService.someMethod(any[MyArgument])).thenReturn(Future.successfull("Some result..."))
```

Other argument matchers:
- `eq`
- `refEq`
- `any`

## Verifying stuff

```scala
verify(myService, times(1)).someMethod(someArgument)

verify(myService, never).someMethod(any[MyArgument]))
```