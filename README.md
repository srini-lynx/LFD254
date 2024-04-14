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
