# Services and Filters

From https://twitter.github.io/finagle/guide/ServicesAndFilters.html

## Services

A Service is just a function. It is the equivalent of a Play Action.

```scala
trait Service[Request, Response] extends (Request => Future[Response])
```

Used to represent both Clients and Servers
- An instance of a Service is used through a Client
- A server implements a Service

## Filters

Used to define application agnostic behaviour. They are also simpple functions.

```scala
abstract class Filter[-RequestIn, +ResponseOut, +RequestOut, -ResponseIn] 
    extends ((RequestIn, Service[RequestOut, ResponseIn]) => Future[ResponseOut])
```

If `RequestIn == RequestOut` and `ResponseIn == ResponseOut` then use `SimpleFilter`:

```scala
trait SimpleFilter[Request, Response] extends Filter[Request, Response, Request, Response]
```

## Composing Filters and Services

Compose filters and services using the `andThen` method

```scala
timeoutFilter.andThen(service)
```