# Play Domain

Classes to understand:
- RequestHeader
- Router
- Handler
- HttpErrorHandler
- HttpConfiguration
- Modules
    - programmatically determines a set of bindings to be used by the application based on Environment and Configuration objects passed as injected arguments.
- HttpFilters
- Environment
    - Captures concerns relating to the classloader and the filesystem for the application. Also has the Mode of the Application (Dev, Test, Prod).
- Configuration
- Writeable
    - Transforms a type `A` to the ByteString associated with a content type

Various terms
- Codec
    Algorithm used to encde/decode data.

Play Components:
- Materializer
- ApplicationLoader
- ApplicationLifecycle
- BuildtInComponents which contains
    - ApplicationLifecycle
    - Configuration
    - Environment
    - HttpFilters
    - Router