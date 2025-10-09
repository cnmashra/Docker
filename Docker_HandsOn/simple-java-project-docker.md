### STEPS TO IMPLEMENT SIMPLE JAVA PROJECT USING DOCKER FILE

```
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % mkdir java-project
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker % cd java-project 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project % git clone https://github.com/LondheShubham153/simple-java-docker.git
Cloning into 'simple-java-docker'...
remote: Enumerating objects: 13, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 13 (delta 1), reused 0 (delta 0), pack-reused 8 (from 1)
Receiving objects: 100% (13/13), done.
Resolving deltas: 100% (1/1), done.
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project % ls
simple-java-docker
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project % cd simple-java-docker 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % ls
Dockerfile README.md  src
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % cat Dockerfile 
# stable official Java runtime base image
FROM openjdk:17-jdk-alpine

# metadata
LABEL maintainer="your-email@example.com"
LABEL version="1.0"
LABEL description="A simple Java application"

# working directory
WORKDIR /app

# Copy source code into the container
COPY src/Main.java /app/Main.java

# Compile the Java code
RUN javac Main.java

# Run the Java application when the container starts
CMD ["java", "Main"]
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % mv Dockerfile Dockerfile-backup
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % ls
Dockerfile-backup README.md         src
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % 
raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % vim Dockerfile


```
