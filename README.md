# Dockerize-Java-REST-API
![1](https://user-images.githubusercontent.com/93249038/215437544-ae7a5577-92eb-469f-9f57-226d46e464b1.jpg)

How To Dockerize Java REST API
A Beginners guide with an example project
 One way is to dockerize the Java REST API and create a docker image so that we can deploy that image any time or sometimes several times a day.


How To Develop and Build Java Rest API
A step by step guide with an example project
medium.com

# Prerequisites
We need to install Docker, maven, java, etc on your machine.

Java
Eclipse IDE
Spring Boot
Maven
Example Project
Here is an example project you can clone and run it on your machine. This is a simple have API with a single endpoint with GET request.


EchoController.java
Here is the Github link for the entire project and you can access the endpoint with this http://localhost:8080/echo/anymessagehere

git clone https://github.com/bbachi/java-api-docker.git

API running on port 8080
Build and Run the Project
Let’s build the project with maven. Make sure you have maven installed on your machine. Check it with this command mvn -v


mvn -v
Once you clone the project and run the following commands to build the project

// clone the project
git clone https://github.com/bbachi/java-api-docker.git
// change the directory
cd java-api-docker
// clean and install
mvn clean install
// Run the application
java -jar target/echo-0.0.1-SNAPSHOT.jar
Once you run the above commands and you can access the API on the port 8080.

# Dockerizing the API
We have seen how to build the project and tun the application in a normal way. Let’ see how we can create a Dockerfile and run the same application in the Docker.

First, let’s create a folder called docker and place the generated war file there with the maven plugin. If you look at the build portion of the pom.xml we have a goal called repackage to place the packaged war file in the docker folder when we build the app. One of the advantages of using a separate folder is that you don’t have to send the entire application code to the Docker daemon when building the image.


build part of pom.xml
Let’s go to the root of the application and run the mvn command mvn clean install. Now we should have the war file in the docker folder.


war file in the docker file
Second, we need to create a Dockerfile that create a Docker image. Here is the file which starts with FROM command and with base image openjdk:8-jre-alpine. Copy the generated war file and finally CMD command that runs when the image is instantiated.


# Dockerfile
Change your directory if you are in the root location and build the docker image and verify with the following commands

// change directory
cd docker
// build the image
docker build -t java-api .
// list the image
docker images
// login into your registry (Docker Hub)
docker login
// tag the image
docker tag java-api <repository name>/java-api
// push the image
docker push <repository name>/java-api
Running The API on Docker
Now, we have the docker image and let's run the container and once it is up and running you can access the api at http://localhost:8080/name/myname.

# // run the container
docker run -d -p 8080:8080 --name javaapi java-api
// list the container
docker ps
// logs
docker logs javaapi
// exec into running container
docker exec -it javaapi /bin/sh

# Running the container
Summary
Docker is an enterprise-ready container platform that enables organizations to seamlessly build, share and run any application, anywhere.
You need to build a war file with the maven plugin.
Create a separate folder for the docker so that you don’t have to send all the source code to the docker daemon.
Use the maven goal called repackage to place the packaged war file in the docker folder.
Always start with the slim Docker image when you are building the image and copy the war file and start the application with java command.
You can tag and push that image into any registry you want with this command docker push
Finally, you can run the docker container with docker run command.
Conclusion
Start running your Java APIs on Docker. This is the simplest configuration while building the Docker images and in future posts, we can see some more complex docker images such as passing profiles, using volumes, etc.

