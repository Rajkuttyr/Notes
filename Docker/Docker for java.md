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

TO push java
need jdk 

```bash
Last login: Fri Jun 19 16:02:23 on ttys000

rajkutty@Rajkuttys-MacBook-Air ~ % docker --version

Docker version 29.5.3, build d1c06ef

rajkutty@Rajkuttys-MacBook-Air ~ % docker run hello-world

Unable to find image 'hello-world:latest' locally

latest: Pulling from library/hello-world

58dee6a49ef1: Pull complete 

c3bdf82c34d1: Download complete 

Digest: sha256:96498ffd522e70807ab6384a5c0485a79b9c7c08ca79ba08623edcad1054e62d

Status: Downloaded newer image for hello-world:latest

  

Hello from Docker!

This message shows that your installation appears to be working correctly.

  

To generate this message, Docker took the following steps:

 1. The Docker client contacted the Docker daemon.

 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.

    (arm64v8)

 3. The Docker daemon created a new container from that image which runs the

    executable that produces the output you are currently reading.

 4. The Docker daemon streamed that output to the Docker client, which sent it

    to your terminal.

  

To try something more ambitious, you can run an Ubuntu container with:

 $ docker run -it ubuntu bash

  

Share images, automate workflows, and more with a free Docker ID:

 https://hub.docker.com/

  

For more examples and ideas, visit:

 https://docs.docker.com/get-started/

  

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES

2fc608b6a121   hello-world   "/hello"   6 minutes ago   Exited (0) 5 minutes ago             vibrant_germain

rajkutty@Rajkuttys-MacBook-Air ~ % docker images

                                                                                **i** Info →   U  In Use

**IMAGE**                **ID**             **DISK USAGE**   **CONTENT SIZE**   **EXTRA**

**hello-world:latest**   96498ffd522e       22.6kB         10.3kB    U   

rajkutty@Rajkuttys-MacBook-Air ~ % docker help

Usage:  docker [OPTIONS] COMMAND

  

A self-sufficient runtime for containers

  

Common Commands:

  run         Create and run a new container from an image

  exec        Execute a command in a running container

  ps          List containers

  build       Build an image from a Dockerfile

  bake        Build from a file

  pull        Download an image from a registry

  push        Upload an image to a registry

  images      List images

  login       Authenticate to a registry

  logout      Log out from a registry

  search      Search Docker Hub for images

  version     Show the Docker version information

  info        Display system-wide information

  

Management Commands:

  agent*      Docker AI Agent Runner

  ai*         Docker AI Agent - Ask Gordon

  builder     Manage builds

  buildx*     Docker Buildx

  compose*    Docker Compose

  container   Manage containers

  context     Manage contexts

  debug*      Get a shell into any image or container

  desktop*    Docker Desktop commands

  dhi*        CLI for managing Docker Hardened Images

  extension*  Manages Docker extensions

  image       Manage images

  init*       Creates Docker-related starter files for your project

  manifest    Manage Docker image manifests and manifest lists

  mcp*        Docker MCP Plugin

  model*      Docker Model Runner

  network     Manage networks

  offload*    Docker Offload

  pass*       Docker Pass Secrets Manager Plugin (beta)

  plugin      Manage plugins

  sandbox*    Docker Sandbox

  scout*      Docker Scout

  system      Manage Docker

  volume      Manage volumes

  

Swarm Commands:

  swarm       Manage Swarm

  

Commands:

  attach      Attach local standard input, output, and error streams to a running container

  commit      Create a new image from a container's changes

  cp          Copy files/folders between a container and the local filesystem

  create      Create a new container

  diff        Inspect changes to files or directories on a container's filesystem

  events      Get real time events from the server

  export      Export a container's filesystem as a tar archive

  history     Show the history of an image

  import      Import the contents from a tarball to create a filesystem image

  inspect     Return low-level information on Docker objects

  kill        Kill one or more running containers

  load        Load an image from a tar archive or STDIN

  logs        Fetch the logs of a container

  pause       Pause all processes within one or more containers

  port        List port mappings or a specific mapping for the container

  rename      Rename a container

  restart     Restart one or more containers

  rm          Remove one or more containers

  rmi         Remove one or more images

  save        Save one or more images to a tar archive (streamed to STDOUT by default)

  start       Start one or more stopped containers

  stats       Display a live stream of container(s) resource usage statistics

  stop        Stop one or more running containers

  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

  top         Display the running processes of a container

  unpause     Unpause all processes within one or more containers

  update      Update configuration of one or more containers

  wait        Block until one or more containers stop, then print their exit codes

  

Global Options:

      --config string      Location of client config files (default "/Users/rajkutty/.docker")

  -c, --context string     Name of the context to use to connect to the daemon (overrides

                           DOCKER_HOST env var and default context set with "docker context use")

  -D, --debug              Enable debug mode

  -H, --host string        Daemon socket to connect to

  -l, --log-level string   Set the logging level ("debug", "info", "warn", "error", "fatal")

                           (default "info")

      --tls                Use TLS; implied by --tlsverify

      --tlscacert string   Trust certs signed only by this CA (default

                           "/Users/rajkutty/.docker/ca.pem")

      --tlscert string     Path to TLS certificate file (default

                           "/Users/rajkutty/.docker/cert.pem")

      --tlskey string      Path to TLS key file (default "/Users/rajkutty/.docker/key.pem")

      --tlsverify          Use TLS and verify the remote

  -v, --version            Print version information and quit

  

Run 'docker COMMAND --help' for more information on a command.

  

For more help on how to use Docker, head to https://docs.docker.com/go/guides/

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                     PORTS     NAMES

2fc608b6a121   hello-world   "/hello"   11 minutes ago   Exited (0) 5 minutes ago             vibrant_germain

rajkutty@Rajkuttys-MacBook-Air ~ % docker rm 2fc608b6a121

2fc608b6a121

rajkutty@Rajkuttys-MacBook-Air ~ % docker run hello-world

  

Hello from Docker!

This message shows that your installation appears to be working correctly.

  

To generate this message, Docker took the following steps:

 1. The Docker client contacted the Docker daemon.

 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.

    (arm64v8)

 3. The Docker daemon created a new container from that image which runs the

    executable that produces the output you are currently reading.

 4. The Docker daemon streamed that output to the Docker client, which sent it

    to your terminal.

  

To try something more ambitious, you can run an Ubuntu container with:

 $ docker run -it ubuntu bash

  

Share images, automate workflows, and more with a free Docker ID:

 https://hub.docker.com/

  

For more examples and ideas, visit:

 https://docs.docker.com/get-started/

  

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps -a          

CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES

e79e25e82017   hello-world   "/hello"   7 seconds ago   Exited (0) 6 seconds ago             determined_kepler

rajkutty@Rajkuttys-MacBook-Air ~ % docker imgaes

docker: unknown command: docker imgaes

  

Run 'docker --help' for more information

rajkutty@Rajkuttys-MacBook-Air ~ % docker images

                                                                                **i** Info →   U  In Use

**IMAGE**                **ID**             **DISK USAGE**   **CONTENT SIZE**   **EXTRA**

**hello-world:latest**   96498ffd522e       22.6kB         10.3kB    U   

rajkutty@Rajkuttys-MacBook-Air ~ % docker rmi 96498ffd522e

Error response from daemon: conflict: unable to delete 96498ffd522e (must be forced) - image is being used by stopped container e79e25e82017

rajkutty@Rajkuttys-MacBook-Air ~ % docker rm e79e25e82017

e79e25e82017

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps -a           

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

rajkutty@Rajkuttys-MacBook-Air ~ % docker rmi 96498ffd522e

Untagged: hello-world:latest

Deleted: sha256:96498ffd522e70807ab6384a5c0485a79b9c7c08ca79ba08623edcad1054e62d

rajkutty@Rajkuttys-MacBook-Air ~ % docker images

                                                                                **i** Info →   U  In Use

**IMAGE**   **ID**             **DISK USAGE**   **CONTENT SIZE**   **EXTRA**

rajkutty@Rajkuttys-MacBook-Air ~ % docker start hello-world

Error response from daemon: No such container: hello-world

failed to start containers: hello-world

rajkutty@Rajkuttys-MacBook-Air ~ % docker create hello-world

Unable to find image 'hello-world:latest' locally

latest: Pulling from library/hello-world

58dee6a49ef1: Pull complete 

c3bdf82c34d1: Download complete 

Digest: sha256:96498ffd522e70807ab6384a5c0485a79b9c7c08ca79ba08623edcad1054e62d

Status: Downloaded newer image for hello-world:latest

dd66e64cb109f648a096df13927be3b6bbf8313b9cef339f8111459379257b69

rajkutty@Rajkuttys-MacBook-Air ~ % docker images

                                                                                **i** Info →   U  In Use

**IMAGE**                **ID**             **DISK USAGE**   **CONTENT SIZE**   **EXTRA**

**hello-world:latest**   96498ffd522e       22.6kB         10.3kB    U   

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS    PORTS     NAMES

dd66e64cb109   hello-world   "/hello"   22 seconds ago   Created             zealous_noyce

rajkutty@Rajkuttys-MacBook-Air ~ % dd66e64cb109

zsh: command not found: dd66e64cb109

rajkutty@Rajkuttys-MacBook-Air ~ % docker rm dd66e64cb109

dd66e64cb109

rajkutty@Rajkuttys-MacBook-Air ~ % docker images

                                                                                **i** Info →   U  In Use

**IMAGE**                **ID**             **DISK USAGE**   **CONTENT SIZE**   **EXTRA**

**hello-world:latest**   96498ffd522e       22.6kB         10.3kB        

rajkutty@Rajkuttys-MacBook-Air ~ % docker rmi 96498ffd522e

Untagged: hello-world:latest

Deleted: sha256:96498ffd522e70807ab6384a5c0485a79b9c7c08ca79ba08623edcad1054e62d

rajkutty@Rajkuttys-MacBook-Air ~ % docker search hello-world

NAME                                DESCRIPTION                                     STARS     OFFICIAL

hello-world                         Hello World! (an example of minimal Dockeriz…   2578      [OK]

rancher/hello-world                 This container image is no longer maintained…   6         

okteto/hello-world                                                                  0         

atlassian/hello-world                                                               3         

goharbor/hello-world                                                                0         

tutum/hello-world                   Image to test docker deployments. Has Apache…   91        

dockercloud/hello-world             Hello World!                                    20        

crccheck/hello-world                Hello World web server in under 2.5 MB          25        

koudaiii/hello-world                                                                0         

ppc64le/hello-world                 Hello World! (an example of minimal Dockeriz…   2         

prajwalendra/hello-world                                                            0         

tsepotesting123/hello-world                                                         0         

infrastructureascode/hello-world    A tiny "Hello World" web server with a healt…   1         

kevindockercompany/hello-world                                                      0         

arm32v7/hello-world                 Hello World! (an example of minimal Dockeriz…   3         

arm64v8/hello-world                 Hello World! (an example of minimal Dockeriz…   3         

cloudflare/hello-world              A simple example application which can be ru…   0         

datawire/hello-world                Hello World! Simple Hello World implementati…   1         

twistlocktest/hello-world                                                           0         

uniplaces/hello-world                                                               0         

wjimenez5271/hello-world                                                            0         

danfengliu/hello-world                                                              0         

lbadger/hello-world                                                                 0         

ansibleplaybookbundle/hello-world   Simple containerized application that tests …   0         

swarna3005/hello-world                                                              0         

rajkutty@Rajkuttys-MacBook-Air ~ % docker pull hello-world

Using default tag: latest

latest: Pulling from library/hello-world

58dee6a49ef1: Pull complete 

c3bdf82c34d1: Download complete 

Digest: sha256:96498ffd522e70807ab6384a5c0485a79b9c7c08ca79ba08623edcad1054e62d

Status: Downloaded newer image for hello-world:latest

docker.io/library/hello-world:latest

  

**What's next:**

    View a summary of image vulnerabilities and recommendations → docker scout quickview hello-world

rajkutty@Rajkuttys-MacBook-Air ~ % docker iamges

docker: unknown command: docker iamges

  

Run 'docker --help' for more information

rajkutty@Rajkuttys-MacBook-Air ~ % docker images

                                                                                **i** Info →   U  In Use

**IMAGE**                **ID**             **DISK USAGE**   **CONTENT SIZE**   **EXTRA**

**hello-world:latest**   96498ffd522e       22.6kB         10.3kB        

rajkutty@Rajkuttys-MacBook-Air ~ % docker create hello-world

9c0ebf41ca2c15b9d7ebd0364fce63f2d5536d3ebaa2e3bacd82b13c1910a17e

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS    PORTS     NAMES

9c0ebf41ca2c   hello-world   "/hello"   23 seconds ago   Created             flamboyant_sutherland

rajkutty@Rajkuttys-MacBook-Air ~ % docker start 9c0

9c0

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

rajkutty@Rajkuttys-MacBook-Air ~ % docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED              STATUS                      PORTS     NAMES

9c0ebf41ca2c   hello-world   "/hello"   About a minute ago   Exited (0) 31 seconds ago             flamboyant_sutherland

rajkutty@Rajkuttys-MacBook-Air ~ %
```


