# LFD254
#Containers for Developers and Quality Assurance
# This repo contins LAB works related to LFD254 of LinuxFoundation.org

# Manually Building docker image and publishing to docker hub
docker run -idt -p 9091:8080 --name dev schoolofdevops/maven:spring bash 
docker ps
pwd
ls
cd spring-petclinic-manual/

==> Login to container with bash
docker exec -it dev bash
==> Check that their is no app directory for the application
ls -altr 

==> Exit the docker container to the host machine
docker exit
==> Copy the source files to the /app Directory inside the container (/app automatically gets created by below command)
docker cp . dev:/app
==> Again check the /app directory and content by logging into the container
docker exec -it dev bash 
==> Exit the container and Check the changes done to the container by below commands
docker exit
docker diff dev
==> Commit the Changes to the container 
docker container commit dev srini78/petclinic:v1
==> Check the image
docker image ls
==> Login to Docker Hub with below command
docker login -u srini78 -p <password> 
==> Push the Changes to docker hub
docker push srini78/petclinic:v1
==> Validated the Image got published from DockerHub End

# Please follow the above steps for the manual build for container


# Added spring-petclinic-dockerfile Directory with same Content, which is Dockerfile approach

But this contains Dockerfile which eventually builds the image in a Declarative way instead of Imperative way in the manual approach
(spring-petclinic-manual)     ==> Imperative Way of Building Docker Image
(spring-petclinic-dockerfile) ==> Declarative Way of Building Docker Image

# After updating the Dockerfile, Please check below steps for the Dockerfile and the container run afterwards

docker image build -t srini78/petclinic:v2 .
[+] Building 191.7s (10/10) FINISHED                                                                                                    docker:default
 => [internal] load build definition from Dockerfile                                                                                              0.0s
 => => transferring dockerfile: 276B                                                                                                              0.0s
 => [internal] load metadata for docker.io/srini78/maven:latest                                                                                   0.0s
 => [internal] load .dockerignore                                                                                                                 0.0s
 => => transferring context: 2B                                                                                                                   0.0s
 => [1/5] FROM docker.io/srini78/maven:latest                                                                                                     0.1s
 => [internal] load build context                                                                                                                 0.0s
 => => transferring context: 1.02MB                                                                                                               0.0s
 => [2/5] WORKDIR /app                                                                                                                            0.0s
 => [3/5] COPY . .                                                                                                                                0.0s
 => [4/5] RUN mvn spring-javaformat:apply && mvn package -DskipTests && mv target/spring-petclinic-2.3.1.BUILD-SNAPSHOT.jar /run/petclinic.jar  189.7s
 => [5/5] WORKDIR /run                                                                                                                            0.0s 
 => exporting to image                                                                                                                            1.7s 
 => => exporting layers                                                                                                                           1.7s 
 => => writing image sha256:06d9d422bf5d8e73ce2e255f20bb7ba77b869b19885902004e3be3c1fefde2de                                                      0.0s 
 => => naming to docker.io/srini78/petclinic:v2      

spring-petclinic-dockerfile$ cat Dockerfile 
FROM srini78/maven

WORKDIR /app

COPY . .

RUN mvn spring-javaformat:apply && \
mvn package -DskipTests && \
mv target/spring-petclinic-2.3.1.BUILD-SNAPSHOT.jar /run/petclinic.jar

EXPOSE 8080

WORKDIR /run

