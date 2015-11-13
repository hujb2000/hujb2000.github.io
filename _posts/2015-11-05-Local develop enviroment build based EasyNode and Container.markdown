---
layout: post
title:  "Build local develop environment based on Docker"
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

In the file /etc/init.d/docker add '--insecure-registry domain:port' to DOCKER_OPTS env.

# Create multi-container applications

You can use a Compose file to configure yur applications's service, Then, using a single command to create and start all the services from your configuration.

Using Compose is basically a three-step process.

1.  Define your app's environment with a Dockerfile so it can be reproduced anywhere.

		FROM mhart/alpine-node
		# FROM mhart/alpine-node:base
		# FROM mhart/alpine-node:base-0.10

		WORKDIR /src
		ADD . .

		# If you have native dependencies, you'll need extra tools
		RUN apk add --update make gcc g++ python

		# If you need npm, don't use a base tag
		RUN npm install

		# If you had native dependencies you can now remove build tools
		RUN apk del make gcc g++ python && \
		  rm -rf /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp

		EXPOSE 3000
		CMD ["npm", "start"]

2.   Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment. docker-compose build the isolated enviromnet.
	 * Each service defined in docker-compose.yml must specify exactly one of image or build .
     * log_driver: "json-file", Only the json-file driver makes the logs availabe directly from docker-compose logs, Using any other(syslog,none)will not
       print any logs
       
3.   Lastly  run docker-compose up and Compose will start an run your entire app.

[Overview Docker Compose](https://docs.docker.com/compose/)

[docker-compose Command](https://docs.docker.com/compose/reference/docker-compose/)

[compose Enviroment variable](https://docs.docker.com/compose/reference/overview/#compose-project-name)

[Compose file reference](https://docs.docker.com/compose/compose-file/)

[multi compose](https://docs.docker.com/compose/extends/#multiple-compose-files)

rules:
Because Docker container names must be unique, you cannot scale a service beyond 1 container if you have specified a custom name. Attempting to do so results in an error.


# Enter Container

Install nsenter, which include in the util-linux issue version.

	cd /tmp
	curl https://www.kernel.org/pub/linux/utils/util-linux/v2.24/util-linux-2.24.tar.gz \
		| tar -zxf-
	cd util-linux-2.24
	./configure --without-ncurses
	make nsenter
	cp nsenter /usr/local/bin

run docker-enter <container id> enter into the container.

On Mac, compile nsenter failed, but now recommend use Docker exec to enter a Docker container, example:

	docker exec -it CONTAINER_NAME /bin/bash

# Dockerfile rules

1. Dockerfile requires strict separation of ENV from the throughtout environment of the image.
Example: such clause: 'EXPOSE 8888; ENV NPM_DEBUG_LEVEL info'  is not permitted to write in the Dockerfile.


12. Dockerfile

docker  build -t repository/tag -f /path/to/a/Dockerfile .

		docker build -t node:0.12.7 -f Dockerfile_node:0.12.7 .
		docker build -t node:0.12.7.cnpm -f Dockerfile_node:0.12.7.ncpm .
		docker build -t node:0.12.7.cnpm.pomelo -f Dockerfile_node:0.12.7.ncpm.pomelo .
		docker build -t node:0.12.7.cnpm.pomelo.src -f Dockerfile_node\:0.12.7.cnpm.pomelo.src .

		docker build -t node:latest.cnpm -f Dockerfile_node\:latest.cnpm .

		docker build -t node:${project_name}.prod .

[Dockerfile_node*](https://github.com/hujb2000/docker_op)

[Docker Volume shared filesystems](https://docs.docker.com/engine/reference/run/#volume-shared-filesystems)

 1. Environment replacement
 The ${variable_name}
 The ${variable:-word} indicates that if variable is set then the result will be that value, if variable is not set when word will be the result
 The ${varivble:+word} indicates that if variable is set the word will be the result ,otherwise the result is the empty string.


 13. Dockerfile Best Practices

[Dockerfile Best Practices](https://docs.docker.com/engine/articles/dockerfile_best-practices/)

The environment variables set using ENV will persist when a container is run from the resulting image. You can view the values using docker inspect, and change them using docker run --env <key>=<value>.

ADD obeys the following rules:

The <src> path must be inside the context of the build; you cannot ADD ../something /something, because the first step of a docker build is to send the context directory (and subdirectories) to the docker daemon.

If <src> is a URL and <dest> does not end with a trailing slash, then a file is downloaded from the URL and copied to <dest>.

If <src> is a URL and <dest> does end with a trailing slash, then the filename is inferred from the URL and the file is downloaded to <dest>/<filename>. For instance, ADD http://example.com/foobar / would create the file /foobar. The URL must have a nontrivial path so that an appropriate filename can be discovered in this case (http://example.com will not work).

If <src> is a directory, the entire contents of the directory are copied, including filesystem metadata.


You can override the ENTRYPOINT instruction using the docker run --entrypoint flag.

The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag. If a user specifies a build argument that was not defined in the Dockerfile, the build outputs an error.

Note: It is not recommended to use build-time variables for passing secrets like github keys, user credentials etc.



export const redis = {
    "sentinels": [
        {"host": "121.40.202.254", "port": 26380},
        {"host": "120.26.112.199", "port": 26380},
        {"host": "120.26.112.207", "port": 26380}
    ],
    name: 'scard-t',
    password: 'zhpwd',
    db: 5
}

export const mongo = {
    "uri": "mongodb://121.40.202.254:50000,120.26.112.199:50000,120.26.112.207:50000/scard_pro",
    "options": {
        "db": {
            "w": 1,
            "wtimeout": 15000,
            "readPreference": "secondaryPreferred",
            "numberOfRetries": "15"
        },
        "user":"scard_pro",
        "pass":"scard_pro",
        "mongos": true,
        "server": {
            "poolSize": 10,
            "socketOptions": { "keepAlive": 1 }
        }
    }
};

var MySQLCluster = require( "ee-mysql-cluster" );




var cluster = new MySQLCluster( [
      timeout: 5000
    , procedures: [ "createTickets", "createLogs" ]
    , functions: [ "deleteLogs" ]
] );


// master, allow 50 concurrent connections
var node = cluster.addNode( {
      host: ""
    , port: 0
    , user: ""
    , pass: ""
    , maxConnections: 50
} );

// slave, allow 2k concurrent connections
var node2 = cluster.addNode( {
      host: ""
    , port: 0
    , user: ""
    , pass: ""
    , readonly: true
    , maxConnections: 2000
} );

ERROR: Cannot start container 62d85673dba5e16bf9ef51c4ffe87b6801b254fe8d1feb10230d4839379ea10b: Cannot link to a non running container: /stkappserverapi_mongo_1 AS /stkappserverapi_app_1/mongo

links:
    - mongo
    - redis
    改成mong2, redis2,就ok了


16. Node5.0.0 通运行babel吗?
cnpm install -g babel-cli 在新的Node5.0.0的版本下不能运行,iojs-3.3.0下运行OK
Docker : node and iojs two officer repostries