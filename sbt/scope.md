# Scopes

A scope is a context. A given key can be defined multiple times, one per every scope.

A list of settings generates a key-value map describing a project.

A full scope is formed of a tuple of a
- project
- configuration 
- task value. 

Global settings can be set at 
- The Build level using ThisBuild. All projects in the build will inherit the settings defined this way. 
```scala 
ThisBuild / name := "walrus"
```
- The Project level if no configuration or task is specified. 
```scala
lazy val myProject = (project in file("my-project")).settings(name := "walrus")
```

### Project 

Define a project by specifying the base directory, configurations, settings, dependencies on other projects etc...

```scala
lazy val myProject = 
    (project in file("my-project"))
        .configs(IntegrationTest, etc...) // Adds configurations to the project
        .settings(...) // Adds/overrides a set of settings
```

### Configuration

Configuration defines a graph of library dependencies, with its own classpath, sources, generated packages, etc...

Configurations can extend other configurations. E.g. Test and IntegrationTest extend RunTime. 