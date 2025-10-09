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
#pull a base image which gives all required tools and libraries
FROM openjdk:17-jdk-alpine

# create a folder where the app code will be started 
WORKDIR /app

# Copy the source code from your HOST machie to your container 
COPY src/Main.java /app/Main.java

# complie the application code
RUN javac Main.java

# run the application
CMD ["java","Main.java"]


raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % cat Dockerfile
#pull a base image which gives all required tools and libraries
#FROM openjdk:17-jdk-alpine ----> Not supporting to my laptop
FROM eclipse-temurin:17-jdk

# create a folder where the app code will be started 
WORKDIR /app

# Copy the source code from your HOST machie to your container 
COPY src/Main.java /app/Main.java

# complie the application code
RUN javac Main.java

# run the application
CMD ["java","Main.java"]

raghavendracn@Raghavendras-MacBook-Pro:~/Documents/Docker/java-project/simple-java-docker % docker build -t java-app .
[+] Building 37.1s (10/10) FINISHED                                                                                       docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                                      0.0s
 => => transferring dockerfile: 460B                                                                                                      0.0s
 => [internal] load metadata for docker.io/library/eclipse-temurin:17-jdk                                                                 3.0s
 => [auth] library/eclipse-temurin:pull token for registry-1.docker.io                                                                    0.0s
 => [internal] load .dockerignore                                                                                                         0.0s
 => => transferring context: 2B                                                                                                           0.0s
 => [1/4] FROM docker.io/library/eclipse-temurin:17-jdk@sha256:8a890d0664b5c3f8bcebd136dc6cdf87ee24b9be3d4c4a952565a4442dcd44e9          33.3s
 => => resolve docker.io/library/eclipse-temurin:17-jdk@sha256:8a890d0664b5c3f8bcebd136dc6cdf87ee24b9be3d4c4a952565a4442dcd44e9           0.0s
 => => sha256:a1873043b7c2b74eea4a7bf3c87f7136a025b79ecc0d122d4ccc69b70f5696a9 143.55MB / 143.55MB                                       32.2s
 => => sha256:8a890d0664b5c3f8bcebd136dc6cdf87ee24b9be3d4c4a952565a4442dcd44e9 8.48kB / 8.48kB                                            0.0s
 => => sha256:1d510963517edb16f8190cbc217446612d770d56b9374bae7dfce4ed035f499e 1.94kB / 1.94kB                                            0.0s
 => => sha256:4ada0181d58d430a6d7367c7a2d5409b8b4d51f021907647d71ba645693d1bb4 6.31kB / 6.31kB                                            0.0s
 => => sha256:7bdf644cff2e9be580c17c3db8d5fc564ad093513bf0fbebebc392c17fa925e5 28.86MB / 28.86MB                                         12.3s
 => => sha256:fdf64b20c10fc3adcde9923aad4855cf5c40adc1ffe2870f710a38ab0a5de2bc 26.38MB / 26.38MB                                         11.2s
 => => sha256:c1851146a2d601e26ceac76ca60ea761f872afd7c7d9505e79420e53c235c96e 159B / 159B                                               11.8s
 => => sha256:22aed5a77a3d19b63a193640b9dd2642a39d97ab78baf043a4ac6d25406f828d 2.28kB / 2.28kB                                           12.3s
 => => extracting sha256:7bdf644cff2e9be580c17c3db8d5fc564ad093513bf0fbebebc392c17fa925e5                                                 0.7s
 => => extracting sha256:fdf64b20c10fc3adcde9923aad4855cf5c40adc1ffe2870f710a38ab0a5de2bc                                                 0.6s
 => => extracting sha256:a1873043b7c2b74eea4a7bf3c87f7136a025b79ecc0d122d4ccc69b70f5696a9                                                 1.0s
 => => extracting sha256:c1851146a2d601e26ceac76ca60ea761f872afd7c7d9505e79420e53c235c96e                                                 0.0s
 => => extracting sha256:22aed5a77a3d19b63a193640b9dd2642a39d97ab78baf043a4ac6d25406f828d                                                 0.0s
 => [internal] load build context                                                                                                         0.0s
 => => transferring context: 280B                                                                                                         0.0s
 => [2/4] WORKDIR /app                                                                                                                    0.3s
 => [3/4] COPY src/Main.java /app/Main.java                                                                                               0.0s
 => [4/4] RUN javac Main.java                                                                                                             0.3s
 => exporting to image                                                                                                                    0.0s
 => => exporting layers                                                                                                                   0.0s
 => => writing image sha256:00a3edf2d16a0c41876330d3c96b3e2c8ddafd9b4a50bc8d9dfd17435fb27ce8                                              0.0s
 => => naming to docker.io/library/java-app                                                                                               0.0s

View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/75fdi8sq9am3wjqdb4zxepp3h

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview 
```
