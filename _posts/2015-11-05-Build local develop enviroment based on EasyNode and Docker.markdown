---
layout: post
title:  "Build local develop environment based on EasyNode and Docker"
date:   2015-11-05 13:35:30
categories: allen.hu update
---

# Install Docker Engine :

[Installation on Max OS X](https://docs.docker.com/engine/installation/mac/)

[Installation on Debian](https://docs.docker.com/engine/installation/debian)

# Install Docker Compose :

[Installation on Debian](https://github.com/docker/compose/releases)

	curl -L https://github.com/docker/compose/releases/download/1.5.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
	chmod +x /usr/local/bin/docker-compose

# Install Docker Machine

[Install Docker Machine](http://docs.docker.com/engine/installation/mac/#from-your-shell)

docker-machine create --driver virtualbox default

docker-machine env default

docker port container'name

docker-machine ip default


eval "$(docker-machine env default)"



Note: Mac X is different to Linux which physical machine is both the localhost and the Docker host.


# Delopy a registry server

create certification：

	mkdir -p certs && openssl req -newkey rsa:4096 -nodes -sha256 -keyout certs/domain.key -x509 -days 10240 -out certs/domain.crt

start yourself registry server:

      docker run -d -p 5000:5000 --restart=always --name registry \
        -v /home/hjb/registry:/var/lib/registry \
        -v /home/hjb/registry_test/certs:/certs \
        -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt \
        -e REGISTRY_HTTP_TLS_KEY=/cert/domain.key \
         registry@2.1.1

start yourself registry server only http:

      docker run -d -p 5000:5000 --restart=always --name registry \
        -v /home/hjb/registry:/var/lib/registry \
         registry@2.1.1

In the file /etc/init.d/docker add '--insecure-registry domain:port' to DOCKER_OPTS env or EXTRA_ARGS .

# Create multi-container applications

You can use a Compose file to configure yur applications's service, Then, using a single command to create and start all the services from your configuration.

[Overview Docker Compose](https://docs.docker.com/compose/)

[docker-compose Command](https://docs.docker.com/compose/reference/docker-compose/)

[compose Enviroment variable](https://docs.docker.com/compose/reference/overview/#compose-project-name)

[Compose file reference](https://docs.docker.com/compose/compose-file/)

[multi compose](https://docs.docker.com/compose/extends/#multiple-compose-files)

# Using Compose is basically a three-step process.

1.  Define your app's environment with a Dockerfile so it can be reproduced anywhere.

		FROM node:latest.babel
        MAINTAINER hujb

        COPY . /usr/src/app

        WORKDIR /usr/src/app
        RUN npm install

        CMD ["./start.sh"]

2.   Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment. docker-compose build the isolated enviromnet.

	 * Each service defined in docker-compose.yml must specify exactly one of image or build .

     * log_driver: "json-file", Only the json-file driver makes the logs availabe directly from docker-compose logs, Using any other(syslog,none)will not
       print any logs
       
3.   Lastly  run docker-compose up and Compose will start an run your entire app.



Dockerfile's Rules:

1. Because Docker container names must be unique, you cannot scale a service beyond 1 container if you have specified a custom name. Attempting to do so results in an error.

2. One Process Per Container

3. Entrypoint must supend

4. Dockerfile requires strict separation of ENV from the throughtout environment of the image. ENV must not write died in the Dockerfile,
   Example: such clause: 'EXPOSE 8888; ENV NPM_DEBUG_LEVEL info'  is not permitted to write in the Dockerfile.

5. Log or Data directory must been mounted by the extra host directory to container.

6. Config must injected by ENV but not local config file

7. Can't work to the directory after it just mounted in the Dockerfile

8. You must change the image's version after anysome modify.


# Enter Container

Install nsenter, which include in the util-linux issue version.

	cd /tmp
	curl https://www.kernel.org/pub/linux/utils/util-linux/v2.24/util-linux-2.24.tar.gz | tar -zxf-
	cd util-linux-2.24
	./configure --without-ncurses
	make nsenter
	cp nsenter /usr/local/bin

run docker-enter <container id> enter into the container.

Compile nsenter failed on Mac Ｘ, but now recommend use Docker exec to enter a Docker container, example:

	docker exec -it CONTAINER_NAME /bin/bash




# A Use case

step 1:

Define a base image to Node.JS program language, write a Dockerfile:latest.label such as:

        FROM node:latest

        RUN npm install -g cnpm --registry=https://r.cnpmjs.org

        #RUN npm config set strict-ssl false
        #RUN npm install -g cnpm --registry=http://r.cnpmjs.org
        #RUN npm install microtime --registry=http://r.cnpmjs.org --disturl=http://dist.cnpmjs.org


        RUN cnpm install -g  pomelo
        RUN cnpm install babel@5.8.29 -g



![Node base image hierarchical tree](/images/NodeImageHierarchicalTree.png)

step 2:

Tag for the base image, such as:

        docker  build -t repository/tag -f /path/to/a/Dockerfile .

        docker build -t node:5.0.0.babel -f Dockerfile:5.0.0.babel .


step 3:

The development stage:

* clone the easynode source code, git clone [easynode](https://github.com/hujb2000/easynode.git)

* coding suite for the following directory structure( you can reference the netease directory)

        bin\             start.sh - run the app   stop.sh - stop the app
        config\          the build-in configurations needs
        src\             source code
        test\            test code
        README.md

* .dockerignore,  ingnore the files or directories to COPY into the images.

* docker-compose.xml

        app:
          dockerfile: "Dockerfile${STAGE}"
          build: .
          volumes:
            - .:/usr/src/app/:rw
          ports:
            - 6005:6005
          dns:
            - 8.8.8.8
          env_file:
            - ./common.env
          environment:
            - ENV=aa
          log_driver: "json-file"
          restart: always

* create build.sh,   build the images for the project

    PRJ='projectname' STAGE='DEVELOPMENT' sh build
    STAGE' value are recommended the following fours: DEVELOPMENT|TEST|PRERELEASE|PRODUCTION

* Define the Dockerfile named DockerfileDEVELOPMENT:

    FROM node:5.0.0.babel

    CMD ["./start.sh"]

* generate development image, The image repository's name will be ${PRJ}${STAGE}_$(servicename), servicename is defined int the docker-compose.yml

    PRJ='projectname' STAGE='DEVELOPMENT' sh build.sh

* RUN program

    docker run -ti|-d -p 6005:6005 -v $PWD:/usr/src/app --workdir=/usr/src/app/netease/bin --env MYSQL_CONFIG_URL='http://106.2.36.81/config.json' projectnamedevelopment_app

* Mac X, Nat forwarding

    docker-machine ip default, 192.168.99.100

    http://192.168.99.100:6005/

    Login into the default VirtualBox VM, use this command 'ifconfig eth0', look for the ip 10.0.2.15, then fill the port forwarding form

    ![port forwarding form](/images/vb_nat.png)


    Now use the Mac X local ip to open the page http://10.0.0.3:6005, show normal. that's ok.

* Mac X, Bridge

    ifconfig eth0

    10.0.0.14

    http://10.0.0.14:6005



step 4.

Test phase:

All the processes are the same as development phase exception for the $PWD and MYSQL_CONFIG_URL env variant.

step 5.

Issue phase:

* Define the Dockerfile named DockerfilePRODUCTION;

        FROM node:5.0.0.babel

        MAINTAINER hujb

        RUN mkdir -p /usr/src/app

        COPY . /usr/src/app

        # run shell script with params
        #RUN /usr/src/app/install.sh


        WORKDIR /usr/src/app
        RUN npm install

        WORKDIR /usr/src/app/netease/bin

        ENTRYPOINT ["./start.sh"]

* generate development image, The image repository's name will be ${PRJ}${STAGE}_$(servicename), servicename is defined int the docker-compose.yml

      PRJ='projectname' STAGE='PRODUCTION' sh build.sh


* tag

  docker tag ${PRJ}${STAGE}_$(servicename) registry.hz.netease.com/${PRJ}${STAGE}_$(servicename):version

* push image

  docker push registry.hz.netease.com/${PRJ}${STAGE}_$(servicename):version

* pull image

  docker pull registry.hz.netease.com/${PRJ}${STAGE}_$(servicename):vlogsersion

* run program

        docker run -d -p 6005:6005 -v $PWD:/usr/src/app/logs --env MSQL_CONFIG_URL='http://w.6go.tv/config.json' 218.205.113.98:5000/uproduction_app



Memoriez:

Machine default already exists.
Starting machine default...
Started machines may have new IP addresses. You may need to re-run the `docker-machine env` command.
Setting environment variables for machine default...

Starting VM...
Too many retries.  Last error: Maximum number of retries (60) exceeded
Started machines may have new IP addresses. You may need to re-run the `docker-machine env` command.
Setting environment variables for machine default...


