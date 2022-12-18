# Theory
*1. What is Docker, and how it differs from dependencies management systems? From virtual machines?*
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications.VMs have the host OS and guest OS inside each VM. A guest OS can be any OS, like Linux or Windows, irrespective of the host OS. In contrast, Docker containers host on a single physical server with a host OS, which shares among them. Sharing the host OS between containers makes them light and increases the boot time.

*2. What are the advantages and disadvantages of using containers over other approaches?*

### The Benefits

a. It is light weight because it does not require any resource pre-allocation (RAM). Whenever it needs resources it acquires them from host OS. It is of less cost. 
b. Continuous integration efficiency – Docker enables you to build a container image and use that same image across every step of the deployment process 
c. Docker has public container registries 
d. It can run on physical hardware, virtual hardware and on cloud. 
e. It takes very less time to create.

### The Downsides
a. It is difficult to manage large amount of containers 
b. Docker does not provide cross-platform compatibility means if an application is designed to run in a Docker container on windows, then it cannot run on Linux Docker container

*3. Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?*
Docker provides the ability to package and run an application in a loosely isolated environment called a container. Container technology is available through the operating system: A container packages the application service or function with all of the libraries, configuration files, dependencies and other necessary parts and parameters to operate. Each container shares the services of one underlying operating system. Docker images contain all the dependencies needed to execute code inside a container, so containers that move between Docker environments with the same OS work with no changes. Docker uses resource isolation in the OS kernel to run multiple containers on the same OS.


Docker ecosystem is composed of the following four components: Docker Daemon (dockerd) Docker Client Docker Images Docker Registries Docker Containers

Docker has a concept of Dockerfile that is used for building the image. A Dockerfile a text file that contains one command (instructions) per line. A docker image is organized in a layered fashion. Every instruction on a Dockerfile is added a layer in an image. The topmost writable layer of the image is a container. Docker Containers are created from existing images. It is a writable layer of the image. Containers can be started, stopped, committed, and terminated. If you terminate a container without committing it, all the container changes will be lost.

*4. Name and describe at least one Docker competitor (i.e., a tool based on the same containerization technology).*
Podman, a container engine developed by RedHat, is one of the most prominent Docker alternatives for building, running, and storing container images. Podman maintains compatibility with the OCI container image spec just like Docker, meaning Podman can run container images produced by Docker and vice versa. Podman’s command line interface is identical to Docker’s, including the arguments.

*4. What is conda? How it differs from apt, yarn, and others?* conda is binary package manager with support for environments.

 # Problem
