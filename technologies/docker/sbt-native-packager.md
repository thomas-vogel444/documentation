# Using sbt-native-packager

From https://medium.com/jeroen-rosenberg/lightweight-docker-containers-for-scala-apps-11b99cf1a666

## Steps

In `project/plugins.sbt` add
```scala
addSbtPlugin("com.typesafe.sbt" % "sbt-native-packager" % "1.2.1")
```

Enable 2 plugins
```scala
enablePlugins(JavaAppPackaging)
enablePlugins(DockerPlugin)
```

Specify the main class to be run by add to your build.sbt file
```scala
mainClass in Compile := Some("com.example.YourMainObject")
```

Build the Docker image by running
```scala
sbt docker:publishLocal
```

Run your image in Docker!
```scala
docker run -rm -p 8080:8080 <projectName>:<version>
```

easy...

## Using Alpine as a base image

Set `dockerBaseImage := "openjdk:jre-alpine"` in build.sbt

Add the folling plugin
```scala
enablePlugins(AshScriptPlugin) 
```