<!-- ---
layout: post
title:  "Scheduler Q4-2015"
date:   2015-11-07 13:35:30
categories: allen.hu update
---
 -->

# 基于蜂巢的全栈服务端解决方案工作计划

## 软件产品设计阶段
   1. 需求分析
   2. 交互设计
   3. 视觉设计

## 软件产品开发阶段


### 基于Docker的本地开发环境搭建

	### MAC下环境搭建 2天
	### Linux下环境搭建  1天
	### Windows下环境搭建 1天

	* 产物： 能开发的本地环境


### 典型Web服务器端开发框架

   * 产物：典型Web应用架构图，各部件实例程序


## 软件产品测试阶段

### 制作镜像

   把本地环境连同代码打包在一个镜像 3天
   蜂巢生产环境未提供功能

   * 产物： 提交可发布的镜像

### 提交镜像  3天

   * 产物： 验证蜂巢自定义发布镜像流程

### 测试镜像   2天



## 运维
   持续集成过程  3天
   水平扩容       5天
   零下线时间部署  15天
   弹性扩容       1个月
   重启策略       5天
   		1. (restart policies build-in)
   性能监控       5天
   故障告警       3天
   回滚          3天
   迭代          3天
   安全（密码通过环境变量）
      1. 密码通过环境变量注入
      2. 文件目录ro,rw两种权限分别注入


## 例子制作

	KOA+NOS+REDIS+RDS+NQS+RPC+MongoDB

   0.  EasyNode框架发布 2天

   1.  KOA+NOS例子 1天

   2.  KOA+REDIS例子 1天

   3.  KOA+RDS例子  1天

   4.  KOA+NQS例子 1天

   5.  KOA+RPC例子 5天

   6.  KOA+Regualar.js 2天

   7.  Gulp打包例子  2天

   8.  KOA+NEJ例子  5天

   9.  KOA+URS   2天

   10. 综合例子    5天

## 标准华开发测试和生产环境
[](http://dockerpool.com/static/books/docker_practice/cases/environment.html)
对于大部分企业来说，搭建 PaaS 既没有那个精力，也没那个必要，用 Docker 做个人的 sandbox 用处又小了点。

可以用 Docker 来标准化开发、测试、生产环境。

企业应用结构

Docker 占用资源小，在一台 E5 128 G 内存的服务器上部署 100 个容器都绰绰有余，可以单独抽一个容器或者直接在宿主物理主机上部署 samba，利用 samba 的 home 分享方案将每个用户的 home 目录映射到开发中心和测试部门的 Windows 机器上。

针对某个项目组，由架构师搭建好一个标准的容器环境供项目组和测试部门使用，每个开发工程师可以拥有自己单独的容器，通过 docker run -v 将用户的 home 目录映射到容器中。需要提交测试时，只需要将代码移交给测试部门，然后分配一个容器使用 -v 加载测试部门的 home 目录启动即可。这样，在公司内部的开发、测试基本就统一了，不会出现开发部门提交的代码，测试部门部署不了的问题。

测试部门发布测试通过的报告后，架构师再一次检测容器环境，就可以直接交由部署工程师将代码和容器分别部署到生产环境中了。这种方式的部署横向性能的扩展性也极好。


service discovery, load balancing and health checks

# 参考
provider by chene

[cloud native application](http://it20.info/2014/12/cloud-native-applications-for-dummies/)

[12 factor](http://12factor.net/zh_cn/)

[docker-base workflow](http://www.luiselizondo.net/a-production-ready-docker-workflow/)







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

Less is More
Slow is Fast
