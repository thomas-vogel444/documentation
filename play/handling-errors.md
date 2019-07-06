# Handling Errors

Two main types of errors:
- client errors
- server errors

Play handles these errors via the `HttpErrorHandler` which defines `onClientError` and `onServerError`.

## Handling errors in a JSON API

By default, the `HttpErrorHandler` returns errors in HTML format.

To use JSON, configure the `play.http.errorHandler` in `application.conf` like

```
play.http.errorHandler = play.api.http.JsonHttpErrorHandler
```

## Extending the default error handler

Play provides `DefaultHttpErrorHandler` with convenience methods that you can override.

See the [docs][https://www.playframework.com/documentation/2.7.x/api/scala/play/api/http/DefaultHttpErrorHandler.html] to see what methods you can override.

## Custom error handler

If using dependency injection, the error handler can be dynamically loaded at runtime.

Either:
- create a class in root package called `ErrorHandler` implementing `HttpErrorHandler`.
- create the same class with a different name in a different package.
    - set the configuration property `play.http.errorHandler` to point to your error handler