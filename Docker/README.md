# Docker Workshop
    1. What is Container and Docker
    2. What is Kubernetes
    3. Workshop
    
## WHat is Container and Docker

Containers such as Docker let us package up entire applications, including the application’s libraries, dependencies, environment and everything else needed by the application to run.

![Image of Docker](/Docker/images/docker.png)

So we can think of containers as portable, packaged bits of functionality and Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. 

Containers isolate the application from the infrastructure beneath so we can run our application on different platforms without having to worry about the underlying systems.
This allows consistency between environments, for example, a container can be easily moved from a development environment to a test environment and then to a production environment. Containers can also be easily scaled in response to increased user load and demand.

To create a Docker container, we will use a Docker image, and to build a Docker image, we will use a Dockerfile. An image is made up of a set of layers and each instruction in a Dockerfile adds a layer to the image.


These images can be stored in a registry for ease of discovery and sharing purposes. Examples of registries include the official Docker Hub registry, or the Amazon EC2 Container Registry or even an internal organisation registry.

An image is essentially a snapshot of a container and a container is a running instance of an image.

![Image of DockerRegistry](/Docker/images/dockerRepository.png)
