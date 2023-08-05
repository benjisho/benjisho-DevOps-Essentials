# Exercise: Getting Started with Docker

In this exercise, you will learn the basics of Docker, including how to create, run, and manage containers. Docker is a powerful tool for containerization, which allows you to package applications and their dependencies into isolated containers, ensuring consistency and portability across different environments.

## Prerequisites

Before you start this exercise, ensure that you have Docker installed on your machine. You can download and install Docker from the official website: [Docker Download](https://www.docker.com/products/docker-desktop)

## Step 1: Running Your First Container

1. Open a terminal or command prompt on your machine.

2. Verify that Docker is installed correctly by running the following command:
```
docker --version
```

4. Pull the official "hello-world" Docker image and run a container from it:
```
docker run hello-world
```

6. Docker will download the "hello-world" image from Docker Hub and run a container displaying a simple message. This confirms that your Docker installation is working.

## Step 2: Creating a Custom Docker Image

1. Create a new directory for your Docker project.

2. Inside the project directory, create a file named "Dockerfile" (without any file extension).

3. Open the "Dockerfile" with a text editor and add the following content:
```
FROM ubuntu:latest

RUN apt-get update && apt-get install -y nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

4. Save the "Dockerfile".

5. Build a Docker image from the "Dockerfile":
```
docker build -t my-nginx-image .
```

7. Run a container from the custom image:
```
docker run -d -p 8080:80 my-nginx-image
```


8. Open your web browser and navigate to `http://localhost:8080`. You should see the default Nginx page, indicating that your custom Nginx container is running successfully.

## Step 3: Managing Containers

1. List all running containers:
```
docker ps
```

3. Stop a running container:
```
docker stop <container_id>
```

5. Remove a container (Note: The container must be stopped before removing):
```
docker rm <container_id>
```

## Conclusion

Congratulations! We've completed the Docker basics exercise.
We've learned how to run a Docker container, create a custom Docker image, and manage containers using basic Docker commands.

# Advanced Exercise: Docker Compose
In this advanced exercise, you will learn how to use Docker Compose to define and manage multi-container applications. Docker Compose is a tool for defining and running multi-container Docker applications using a YAML file to configure the services, networks, and volumes required for your setup.

## Prerequisites
Before you start this advanced exercise, make sure you have completed the "Getting Started with Docker" exercise.

## Step 1: Create a Docker Compose File
1. Create a new directory for your Docker Compose project.

2. Inside the project directory, create a file named "docker-compose.yml".

3. Open the "docker-compose.yml" with a text editor and add the following content:
```
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
```
4. Save the "docker-compose.yml".

## Step 2: Start Docker Compose
1. Open a terminal or command prompt on your machine.

2. Navigate to the directory containing the "docker-compose.yml" file.

3. Start the Docker Compose setup:
```
docker-compose up -d
```
5. Docker Compose will download the Nginx image and start the container.

6. Open your web browser and navigate to http://localhost:8080. You should see the default Nginx page, indicating that your Nginx container started successfully using Docker Compose.
## Step 3: Stop and Clean Up
1. To stop the Docker Compose setup, run the following command:
```
docker-compose down
```
2. Docker Compose will stop and remove the containers defined in the "docker-compose.yml" file.

## Conclusion
Congratulations! We've completed the Docker Compose exercise.
We've learned how to define and manage multi-container applications using Docker Compose. Docker Compose simplifies the process of running complex applications with multiple services, making it easier to maintain and scale containerized applications.
