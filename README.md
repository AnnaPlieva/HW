# Theory
*1. What is Docker, and how it differs from dependencies management systems? From virtual machines?*

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications.VMs have the host OS and guest OS inside each VM. A guest OS can be any OS, like Linux or Windows, irrespective of the host OS. In contrast, Docker containers host on a single physical server with a host OS, which shares among them. Sharing the host OS between containers makes them light and increases the boot time.

*2. What are the advantages and disadvantages of using containers over other approaches?*

### The Benefits

a. It is light weight because it does not require any resource pre-allocation (RAM). Whenever it needs resources it acquires them from host OS. It is of less cost. 

b. Continuous integration efficiency – Docker enables you to build a container image and use that same image across every step of the deployment process 

c. Docker has public container registries 

d. It can run on physical hardware, virtual hardware and on cloud

e. It takes very less time to create.

### The Downsides

a. It is difficult to manage large amount of containers 

b. Docker does not provide cross-platform compatibility means if an application is designed to run in a Docker container on windows, then it cannot run on Linux Docker container

*3. Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?*

Docker provides the ability to package and run an application in a loosely isolated environment called a container. Container technology is available through the operating system: A container packages the application service or function with all of the libraries, configuration files, dependencies and other necessary parts and parameters to operate. Each container shares the services of one underlying operating system. Docker images contain all the dependencies needed to execute code inside a container, so containers that move between Docker environments with the same OS work with no changes. Docker uses resource isolation in the OS kernel to run multiple containers on the same OS.

  ![image](https://user-images.githubusercontent.com/120120242/208312311-a6032da1-264b-4736-b191-54e58dcdf6e9.png)

Docker ecosystem is composed of the following four components: Docker Daemon (dockerd) Docker Client Docker Images Docker Registries Docker Containers

Docker has a concept of Dockerfile that is used for building the image. A Dockerfile a text file that contains one command (instructions) per line. A docker image is organized in a layered fashion. Every instruction on a Dockerfile is added a layer in an image. The topmost writable layer of the image is a container. Docker Containers are created from existing images. It is a writable layer of the image. Containers can be started, stopped, committed, and terminated. If you terminate a container without committing it, all the container changes will be lost.

*4. Name and describe at least one Docker competitor (i.e., a tool based on the same containerization technology).*

Podman, a container engine developed by RedHat, is one of the most prominent Docker alternatives for building, running, and storing container images. Podman maintains compatibility with the OCI container image spec just like Docker, meaning Podman can run container images produced by Docker and vice versa. Podman’s command line interface is identical to Docker’s, including the arguments.

*4. What is conda? How it differs from apt, yarn, and others?* conda is binary package manager with support for environments.

 # Problem
 ### Conda

             conda create  -n annenv
             conda config --add channels defaults
             conda config --add channels bioconda
             conda config --add channels conda-forge
  
             conda config --set channel_priority strict
             conda activate annenv
             #install
             conda install fastqc =0.11.9
             conda install star=2.7.10b
             conda install samtools=1.16.1
             conda install salmon=1.9.0
             conda install bedtools=2.30.0
             conda install multiqc=1.13
             conda install picard=2.27.5
             #export my env 
             conda env export --from-history > myannenv.yml
             conda env export > myannenv2.yml
             #rebuilt environment
             conda env create --name myannev_env_2 -f   myannenv2.yml
             
### Docker            

              FROM ubuntu:22.04

              #  version for STAR
              ARG STAR_VERSION=2.7.10b
              # create variable with necessery libraries for STAR and samtools
              ENV PACKAGES gcc g++ make wget zlib1g-dev unzip libncurses5-dev libbz2-dev liblzma-dev \
              libcurl4-gnutls-dev libssl-dev perl bzip2 gnuplot ca-certificates gawk git ant

              RUN set -ex

              # downloading and installing packages for installing and compiling libraries
              RUN apt-get update && \
                  apt-get install -y --no-install-recommends ${PACKAGES} && \
                  apt-get clean && \
                  g++ --version && \
                  cd /home && \
              # downloading, unpacking, making STAR package
                  wget --no-check-certificate https://github.com/alexdobin/STAR/archive/${STAR_VERSION}.zip && \
                  unzip ${STAR_VERSION}.zip && \
                  cd STAR-${STAR_VERSION}/source && \
                  make STARstatic && \
              # creating dir for executive and copy it to this dir
                  mkdir /home/bin && \
                  cp STAR /home/bin && \
                  cd /home && \
              # removing archive
                  'rm' -rf STAR-${STAR_VERSION}

              # version for samtools
              ARG SAMTOOLSVER=1.16.1

              # downloading, unpacking, removing archive, making and installing samtools
              RUN wget https://github.com/samtools/samtools/releases/download/${SAMTOOLSVER}/samtools-${SAMTOOLSVER}.tar.bz2 && \
               tar -xjf samtools-${SAMTOOLSVER}.tar.bz2 && \
               rm samtools-${SAMTOOLSVER}.tar.bz2 && \
               cd samtools-${SAMTOOLSVER} && \
               ./configure && \
               make && \
               make install && \
               mkdir /data

              # java for fastqc
              RUN apt-get install -y default-jre

              # downloading and uzipping FastQC
              ADD http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.9.zip /tmp/
              RUN unzip /tmp/fastqc_v0.11.9.zip && sed -i 's/Xmx250m/Xmx2048m/' FastQC/fastqc && chmod 755 FastQC/fastqc && \
              ln -s /FastQC/fastqc /home/bin/fastqc && rm -rf /tmp/fastqc_v0.11.9.zip

              # downloading and installing picard
              RUN git clone https://github.com/broadinstitute/picard.git && cd /picard
              RUN cd picard/ && ./gradlew shadowJar

              # downloading, unpacking and installing bedtools, removing acrhive afterwards
              RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.30.0/bedtools-2.30.0.tar.gz
              RUN apt-get install -y python-is-python3
              RUN tar -zxvf bedtools-2.30.0.tar.gz
              RUN cd bedtools2 && \
               make  
              RUN rm -rf bedtools-2.30.0.tar.gz
              # adding rights to bedtools bins and coping them to /home/bin/
              RUN cd bedtools2/bin && chmod a+x $(ls) && cp $(ls) /home/bin/

              # downloading salmon 1.9.0
              ADD https://github.com/COMBINE-lab/salmon/releases/download/v1.9.0/salmon-1.9.0_linux_x86_64.tar.gz /tmp/
              RUN tar -zxvf /tmp/salmon-1.9.0_linux_x86_64.tar.gz

              # installing pip and multiqc
              RUN apt-get update && apt install -y python3-pip
              RUN pip3 install multiqc==1.13

              # continuing building salmon
              RUN git clone https://github.com/oneapi-src/oneTBB.git
              RUN apt-get install -y cmake
              RUN cd salmon-1.9.0_linux_x86_64 && mkdir build && cd build && cmake -DFETCH_BOOST=TRUE -DTBB_INSTALL_DIR=../../oneTBB  ../../oneTBB && make && make install
              # add salmon bin to docker bin
              RUN cd salmon-1.9.0_linux_x86_64/bin/ && chmod a+x salmon && cp salmon /home/bin/

              # this line was for removing installing libraries, but it was commented because some packages do not work without some of them
              # so PACKAGES variable should be manually sorted out before removing
              # RUN  apt-get --purge autoremove -y  ${PACKAGES}

              # add bin dir to PATH
              ENV PATH /home/bin:${PATH}


              # add labels
              LABEL author="Anna Plieva" \
                    maintainer="plieva.09@bk.ru"
                    
                    
 ##
               # building image from Dockerfile
              sudo docker build -t anna_image .

              # run container from image
              docker run -dp 3000:3000 anna_image
                    
