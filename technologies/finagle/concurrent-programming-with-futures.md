# Concurrent Programming with Futures

From https://twitter.github.io/finagle/guide/Futures.html

`com.twitter.util.Future` is essentially the same as a `scala.concurrent.Future`. Think of Future as a featherweight thread.

## Blocking or synchronous work

Use `com.twitter.util.FuturePool` for blocking code. This manages a pool of threads dedicated to the blocking operations. Your other `Futures` won't be affected.

```scala
import com.twitter.util.{Future, FuturePool}

def someIO(): String = ???

val futureResult: Future[String] = FuturePool.unboundedPool {
  someIO()
}
```

## Future as containers

3 states:
- Empty (pending)
- Succeeded (with a result of type T)
- Failed (with a Throwable)

Register a callback instead of querying the state:

```scala
val f: Future[Int] = ???

f.onSuccess { result: Int =>
  println("The result is " + result)
}
```

Or for failures:
```scala
f.onFailure { cause: Throwable =>
  println("f failed with  " + cause)
}
```

## Sequential Conposition

Use the usual:
- `map`
- `flatMap`
- `Future.collect` === `Future.sequence`

## Recover from failure

```scala
f.rescue {
    case: TimeoutException => ???
}
```