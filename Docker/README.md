# Docker Workshop
    1. What is Container and Docker
    2. What is Kubernetes
    3. Workshop
    
## What is Container and Docker

Containers such as Docker let us package up entire applications, including the application’s libraries, dependencies, environment and everything else needed by the application to run.

![Image of Docker](/Docker/images/docker.png)

So we can think of containers as portable, packaged bits of functionality and Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. 

Containers isolate the application from the infrastructure beneath so we can run our application on different platforms without having to worry about the underlying systems.
This allows consistency between environments, for example, a container can be easily moved from a development environment to a test environment and then to a production environment. Containers can also be easily scaled in response to increased user load and demand.

To create a Docker container, we will use a Docker image, and to build a Docker image, we will use a Dockerfile. An image is made up of a set of layers and each instruction in a Dockerfile adds a layer to the image.


These images can be stored in a registry for ease of discovery and sharing purposes. Examples of registries include the official Docker Hub registry, or the Amazon EC2 Container Registry or even an internal organisation registry.

An image is essentially a snapshot of a container and a container is a running instance of an image.

![Image of DockerRegistry](/Docker/images/dockerRepository.png)

## What is Kubernetes

Kubernetes,is a system for running and coordinating containerized applications across a cluster of machines. It is a platform designed to completely manage the life cycle of containerized applications and services using methods that provide predictability, scalability, and high availability.

As a Kubernetes user, you can define how your applications should run and the ways they should be able to interact with other applications or the outside world. You can scale your services up or down, perform graceful rolling updates, and switch traffic between different versions of your applications to test features or rollback problematic deployments. Kubernetes provides interfaces and composable platform primitives that allow you to define and manage your applications with high degrees of flexibility, power, and reliability.

## Workshop (Dockerizing the node.js app)
1. Clone the node-tutorial project and follow the readme.md steps.
2. Dockerize the application
    To run this application in a Docker container, we will write a Dockerfile using the official node image from the Docker Hub registry. We will then use Docker Compose, a tool for running multi-container applications, to spin up our containers and run our app.
    a. create a Dockerfile in the project directory.
            FROM node:latest
            RUN mkdir -p /usr/src/app
            WORKDIR /usr/src/app
            COPY package.json /usr/src/app/
            RUN npm install
            COPY . /usr/src/app
            EXPOSE 3009
            CMD [ “npm”, “start” ]
    b.  Dockerize MongoDB
        We could build our own mongo image but wherever possible, we should look to use official images.
        This is beneficial as it saves us a fair amount of time and effort — we don’t have to spend time creating our own images or worry about the latest releases or applying updates. All of that is taken care of by the publisher of the image.
    
        Let’s add a docker-compose.yml file to define the services in our application.
            version: "2"
            services:
              app:
                container_name: app
                restart: always
                build: .
                ports:
                  - "3000:3000"
                links:
                  - mongo
              mongo:
                container_name: mongo
                image: mongo
                volumes:
                  - ./data:/data/db
                ports:
                  - "27017:27017"
