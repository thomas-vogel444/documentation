# Projects

# Directory Structure

The base directory is the root directory of your project. For instance the following has the base directory in `/my-project`

```scala
lazy val myProject = (project in file("my-project"))
```

SBT operates by convention. It assumes that every project will have the same struture as Maven for source files.

```
src/
    main/
        resources/
        scala/
    test/
        resources/
        scala/
```


Define a project using the following notation:



The `sbt` and `Keys` packages are automatically imported.

Naming:
- Build
- Project (referred to as subproject in the sbt documentation)
- Configuration
- Setting (Key-value pairs of Keys and tasks/values)