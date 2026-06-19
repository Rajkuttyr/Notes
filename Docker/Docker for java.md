Build application and millions of people use
Before docker we had virtualisation 

Contenarisation
Contaniner manages the application enable the app to run on multiple device 
Support scalablity and portablity 
Packages of software and ship it to the other machine
Docker is a tool for containersaition
Components
Docker Engine - creating and managing container
User interact with comands
Images - blueprint , light weight file of the container 
Docker file 
Docker hub - contains all the images of the popular service
Container has network protocols
and network components
Docker has volume to store data
Docker compose helps dockers to communicate

```bash
docker run {image name}
```

user to check the containers that are currently running
```bash
docker ps
```
 
 to check all the  container
 ```bash
 docker ps -a
 ```
 
 to check the docker images
 
 ```bash
 docker images
 ```
 
 remove the contianer
 
 remover the images
 
 steps1
 1. Docker Search 
    ```bash
    docker search imagename
    ```
   
   2. Docker pull 
      ```bash
      Docker pull imagename
      ```

 3. Docker create -creates container
    ```bash
    docker create image id
    ```
    
  4. docker start - start the container
     ```bash
     docker start container id
     ```
     
  5. docker stop - to stop the container
 6. docker pause 
    
    docker run all the above steps
    
Docker Architecture
Client ->Docker client ->Docker[Image Container Volumes Deamon] ->Registery
Docker Deamon -> exectues the background task search images get pull create container are managed by deamon 

