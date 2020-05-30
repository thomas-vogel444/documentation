# Concepts

- ActorSystem
    - Class responsible for creating Actors
- Graph
    - Description of the stream to be created
- Materializer
    - Interprets the graph and creates the actor structure executing the stream using the ActorSystem.
- Dispatcher
    - Akka's implementation of an ExecutionContext
    - Responsible for selecting an actor and it's messages and assigning them the CPU.