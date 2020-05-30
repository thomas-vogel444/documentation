# Dependency Injection

From https://www.playframework.com/documentation/2.6.x/ScalaDependencyInjection

## BuiltInModule

Play provides a shit ton of components to inject in your own components which are bound in [`BuildInModule`][https://github.com/playframework/playframework/blob/2.6.x/core/play/src/main/scala/play/api/inject/BuiltinModule.scala].

Useful ones include:
- Environment
- Configuration
- HttpConfiguration
- PlayBodyParsers
- ControllerComponents
- Futures for configuring timeouts on Futures
- ApplicationLifecycle
- ExecutionContext
- HttpErrorHandler
- HttpRequestHandler

## Specifying Controllers in the routes file

2 ways of doing it
- via DI
    - Generated Route class get injected the controllers specified
- via static Action methods
    - Not recommended. Only for legacy reasons.

## Component Lifecycle

Components are 
- created every time one is injected.
    - use @Singleton to create only one
- created lazily as needed
    - specify an eager binding in a AbstractModule.
- not cleaned up once the Application stops
    - inject an ApplicationLifeCycle in your component and add a stopHook to it

## Custom Bindings

Create a trait for your component to be injected and have user classes depend on that trait.

If writing an application, specify the implementation either via
- Binding annotations for simple use case, i.e. one implementation.
    ```scala
    @ImplementedBy(classOf[MyComponentImpl])
    ````
- Programmatic bindings for more complex cases, i.e. multiple implementations dependent on configuration.
    - Create a class extending AbstractModule with Environment and Configuration as injected arguments
    - bindings can be specified in 2 ways
        - directly
        ```scala
        bind(classOf[Walrus]).to(classOf[WalrusImpl])
        ```
        - via a `Provider`
        ```scala
        bind(classOf[Walrus]).toProvider(WalrusProvider)
        ```

If writing a library, specify the implementation by creating a class extending Module with Environment and Configuration as injected arguments

## Advanced

You can change how the app is build by creating a custom GuiceApplicationLoader. You will need to specify it in the config via the field `play.application.loader`