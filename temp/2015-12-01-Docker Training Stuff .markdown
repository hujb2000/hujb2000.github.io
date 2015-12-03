
layout: post
title:  "Docker Training's Stuff"
date:   2015-12-01 13:35:30
categories: allen.hu update
---


# Docker基础篇

## Docker简介

Docker是一个开源项目，诞生于2013年初，最初是dotCloud公司内部的一个业务项目。它基于Google公司推出的Go语言实现。项目后来加入Linux基金会，遵从了Apache 2.0协议，项目代码而[GitHub](https://github.com/docker/docker)上进行维护。


Docker项目的目标是实现轻量级的操作系统虚拟化解决方案，Docker的基础是Linux容器(LXC)等技术。在LCX的基础上Docker进行了进一步的封装，让用户不需要关心容器的管理，使得操作更为简便，用户操作Docker的容器就像操作一个快速轻量级的虚拟机一样简单。


## Docker与VM对比

作为一种新兴的虚拟化方式，Docker 跟传统的虚拟化方式相比具有众多的优势。

首先，Docker 容器的启动可以在秒级实现，这相比传统的虚拟机方式要快得多。 其次，Docker 对系统资源的利用率很高，一台主机上可以同时运行数千个 Docker 容器。

容器除了运行其中应用外，基本不消耗额外的系统资源，使得应用的性能很高，同时系统的开销尽量小。传统虚拟机方式运行 10 个不同的应用就要起 10 个虚拟机，而Docker 只需要启动 10 个隔离的应用即可。

具体说来，Docker 在如下几个方面具有较大的优势。

更快速的交付和部署

对开发和运维（devop）人员来说，最希望的就是一次创建或配置，可以在任意地方正常运行。

开发者可以使用一个标准的镜像来构建一套开发容器，开发完成之后，运维人员可以直接使用这个容器来部署代码。 Docker 可以快速创建容器，快速迭代应用程序，并让整个过程全程可见，使团队中的其他成员更容易理解应用程序是如何创建和工作的。 Docker 容器很轻很快！容器的启动时间是秒级的，大量地节约开发、测试、部署的时间。

更高效的虚拟化

Docker 容器的运行不需要额外的 hypervisor 支持，它是内核级的虚拟化，因此可以实现更高的性能和效率。

更轻松的迁移和扩展

Docker 容器几乎可以在任意的平台上运行，包括物理机、虚拟机、公有云、私有云、个人电脑、服务器等。 这种兼容性可以让用户把一个应用程序从一个平台直接迁移到另外一个。

更简单的管理

使用 Docker，只需要小小的修改，就可以替代以往大量的更新工作。所有的修改都以增量的方式被分发和更新，从而实现自动化并且高效的管理。


![Docker与VM对比](/images/dockervm.png)
![Docker与VM对比](/images/dockervm2.png)


## Docker对开发流程的再造

通过docker run –v 将用户的home目录映射到容器中，需要提交测试时，只需要将代码移交给测试部门，然后分配一个容器使用-v加载测试部门的home目录启动后即可。这样，在公司内部的开、测试基本就统一了，不会出现开发部门提交的代码，测试部门部署不了的问题。
测试部门发布测试通过的报告后，架构师再一次检测容器环境，就可以直接交由部署工程师将代码和容器分别部署到生产环境中了。这种方式的部署横向性能的扩展性也极好。
评估Docker的安全性时，主要考虑以下三个方面
由内核的名字空间和控制组机制提供的容器内在安全
Docker程序（特别是服务端）本身的抗击性
内核安全性的加强机制对容器安全性的影响
Docker服务端的防护
Docker服务的运行目前需要root权限，因此其安全性十分关键，VPN或SSL来限制，最近改进的Linux名字空间机制将可以实现使非root用衣来运行全功能的容器，这将从根本上解决了容器和主机之间共享文件系统而引起的安全问题。
管理工具nrpe,collectd  ，  Apparmor, SELinux, GRSEC来增强安全性
内核能力机制



## Docker基本概念

* Docker Client
* Docker Daemon
* Docker Hub/Docker Registry/Docker private

仓库是集中存放镜像文件的场所。仓库注册服务器上往往存放这多个仓库，每个仓库中又包含了多个镜像，每个镜像有不同的标签(tag)
仓库分为公开仓库(public)和私有仓库(private)两种形式
用户创建了自己的镜之后就可以使用push命令将它上传到公有和私有仓库，这另外地方可以pull下来。


* Docker 镜像
	Docker镜像就是一个只读的模板，可以用来创建容器，Docker提供了一个很简单的机制来创建镜像或者更新现有的镜像，用户甚至可以直接从其他人那里上载一个已经做好的镜像来直接使用。

* Docker 容器

	容器是从镜像创建的运行实例，它可以被启动、开始、停止、删除。每个容器都是相互隔离的，保证安全的平台
    可以把容器看做是一个简易版的Linux环境(包括root用户权限、进程空间、用户空间和网络空间等)和运行在其中的应用程序。

* 容器原理
* 容器的隔离性
* cgroups
* Docker 分层存储(AUFS)



借助于namespace的隔离机制和cgroup限额功能，LXC提供了一套统一的API和工具来建立和管理container, LXC利用了如下 kernel 的features:
Kernel namespaces (ipc, uts, mount, pid, network and user)
Apparmor and SELinux profiles
Seccomp policies
Chroots (using pivot_root)
Kernel capabilities
Control groups (cgroups)
LXC 向用户屏蔽了以上 kernel 接口的细节, 提供了如下的组件大大简化了用户的开发和使用工作:
The liblxc library
Several language bindings (python3, lua and Go)
A set of standard tools to control the containers
Container templates


## Docker常用命令

* 安装

Debian8.0 Jessie(64-bit)
Debian 7.7 Wheezy(64-bit)
/etc/apt/sources.list
deb  http://http.debian.net/debian wheezy-backports main
apt-get  update
apt-get install –t wheezy-backports linux-image-amd64
Restart system(uname –a前3.2.0-4-amd64 Debian3.2.65,后3.16.0,Debian3.16.7）
curl –sSL https://get.docker.com/ | sh
service docker restart

Giving non-root access
Groupadd docker
Gpasswd –a ${user} docker
service docker restart

* 拉取镜像

从仓库获取镜像
Docker search redis
Docker pull redis@latest
修改已有镜像docker run –t –i  redis  /bin/bash
Docker commit – m ‘added json’ –a ‘hujb2000’  redis  redis8.8.8(-m指定提交的说明，-a可以指定更梳妆打扮的用户信息，之后是用来创建镜像的容器的ID，最后指定目标镜像的仓库名和tag信息)
Docker run –t –i  redis2 /bin/bash

利用Dockerfile来创建镜像
Mkdir redis_rep, cd redis_rep, touch Dockerfile
#使用来注释
FROM指令告诉Docker使用哪个镜像作为基础
接着是维护者的信息
RUN开头的指令会在创建中运行，比如安装一个软件包，在这里使用apt-get 来安装
Docker build –t=“redis2” .(-t标记来添加tag,指定新的镜像用户信息，.是Dockerfile所在的路径)
Docker tag redis-ori redis-tar(tag修改标签)
从本地文件系统导入镜像
Docker push username/repos
存出镜像：docker save –o a.tar redis2
载入镜像：docker load –input a.tar
Docker rmi 移除镜像，docker rm移除容器


* 给镜像打TAG
* 提交镜像
* PUSH镜像
* 运行镜像
*

## Dockerfile制作原则与规则

Dockerfile是一个镜像的表示，可以通过Dockerfile来描述构建镜像的步骤，并自动构建一个容器

## Docker底层实现

基本架构，Docker采用了C/S架构，包括客户端与服务端，Docker daemon作为服务端接受来自客户的请求，并处理这些请求(创建、运行、分发容器),客户端和服务端既可以运行在一个机器上，也可以通过socket或者restful api来进行通信。
Docker网络实现，Docker中的网络接口默认都是虚拟的接口，Linux通过在内核中进行数据复制来实现虚拟接口之间的数据转发，发送接口的发送缓存中的数据包被直接复制到接收接口的接收缓存中。
Etcd是CoreOS团队发起的一个管理配置信息和服务发现的项目，于2013年6月发起的开源项目，它的目标是构建一个高可用的分布式键什数据库,基于Go实现，
受到Apache Zookeeper和doozer项目的启发，etcd设计时考虑下面四个要素
支持REST风格
支持HTTPS
支持并发1k/s的写操作
支持分布式结构，基于Raft的一致性算法
可以设置目录

用户需要考虑虚拟化方法，尤其是硬件虚拟化方法，需要借助其解决以下四个问题
隔离性，每个用户实例之间的相互隔离，硬件虚拟化方法给出的方法是VM,LVC给出的方法是container,更细一点是kernel namespace
可配额/可度量，每个用户实例可以按需要提供其计算资源，所使用的资源可以被计量。硬件虚拟化方法因为虚拟了CPU，memory可以方便实现，LVC则主要利用cgroups来控制资源
移动性，用户的实例可以很方便地复制、移动、重建。硬件虚拟化方法提供snapshot和image来实现，docker主要利用AUFS实现
安全性，这个话题比较大，这里强调host主机的角度尽量保护contaier。硬件虚拟化的方法因为虚拟化的水平比较高，用户进程都是在KVM等虚拟机容器中翻译进行的，然而对于LVC，用户的进程是lxc-start进程的子进程，只是而Kernel的namespace中隔离的，因此需要一些kernel的patch来保证用户的运行环境不会受到来自host主机的恶意入侵，
Linux Namespace(ns)
LXC所实现的隔离性主要来自kernel的namespace,其中pid,net,ipc,mnt,uts等namespace将container的进程，网络，消息，文件系统和hostname隔离开。


Pid namespace
用户进程是lxc-start进程的子进程，不同用户的进程就是通过pid namespace隔离开的，且不同namespace中可以有相同PID,具有以下特征：
1、每个namespace中的pid是有自己的pid=1的进程(类似/sbin/init进程）
2、每个namespace中的进程只能影响自己的同一个namespace或子namespace中的进程
3、因为/proc包含正在运行的进程，因此而container中的pseudo-filesystem的/proc目录只能看到自己namespace中的进程
4、因为namespace允许嵌套，父进程可以影响子namespace进程，所以子namespace的进程可以在父namespace中看到，但是具有不同的pid
Net namespace
有了pid namespace ,每个namespace中的pid能够相互隔离，但是网络端口还是共享host的端口。网络隔离是通过netnamespace实现的，每个net namespace有独立的network devices, IP address, IP routing tables, /proc/net目录，这样每个container的网络就能隔离开来，LXC在此基础上有5种网络类型，docker默认采用veth的方式将container中的虚拟网卡同host上的一个docker bridge连接在一起


IPC namespace
Container中进程交互还是采用linux常见的进程间交互方法(interprocess communication-IPC)包括常见的信号量、消息队列、内存共享。然而同VM不同，container的进程交互实际是host具有相同pid namespace中的进程间交互，因此需要在IPC资源申请时加入namespace信息，每个IPC资源有一个唯一的32bit ID
Mnt namespace
类似chroot ,将一个进程放到一个特定的目录执行，mnt namespace允许不同namespace的进程看到的文件结构不同，这样每个namespace中的进程所看到的文件目录被隔离开了，同chroot不同，每个namespace中的container在/proc/mounts的信息只包含所在namespace 的mount point
Uts namespace
UTS(UNIX Time sharing System）namespace允许每个container拥有独立地hostname和domain name,使其在网络上被视作一个独立的节点而非Host上的一个进程
User namespace
每个container可以有不同的user和group id ,也就是说可以container内部的用户在container内部执行程序而非 Host上的用户

Cgroups实现了对资源的配额和度量。Cgroups的使用非常简单，提供类似文件的接口，在/cgroup目录下新建一个文件夹即可新建一个group，在此文件夹中新建task文件，并将pid写入该文件，即可实现对该进程的资源控制，具体的资源配置项可以而该文件夹中新建子subsystem,{子系统前缀}.{资源项}是典型的配置方法，如memory.usage_in_bytes就定义了该group在subsystem memory中的一个内存限制选项。另外,cgroups中的subsystem可以随意组合，一个subsystem可以在不同的group中，也可以一个group包含多个subsystem。
CPU:在cgroup中，并不能像硬件虚拟化防范一样能够定义CPU能力，但能够定义CPU的轮转优先级
Cpusets: cpusets定义有几个CPU可以被这个group使用，或者哪几个CPU可以供这个group使用，在某些场景下，单CPU绑定可以防止多核间缓存切换，从而提高效率。
Memory:
Blkio: block IO相关的统计和限制，byte/operation统计和限制(IOPS等)，读写速度限制，但是这里统计的都是同步IO
Net_cls, cpuacct,devices, freezer等其它可管项


借助于namespace的隔离机制和cgroup限额功能，LXC提供了一套统一的API和工具来建立和管理container, LXC利用了如下 kernel 的features:
Kernel namespaces (ipc, uts, mount, pid, network and user)
Apparmor and SELinux profiles
Seccomp policies
Chroots (using pivot_root)
Kernel capabilities
Control groups (cgroups)
LXC 向用户屏蔽了以上 kernel 接口的细节, 提供了如下的组件大大简化了用户的开发和使用工作:
The liblxc library
Several language bindings (python3, lua and Go)
A set of standard tools to control the containers
Container templates






## Docker局限

Docker是基于Linux 64bit的，无法而windows/unix或32bit的linux环境下使用
LCX是基于cgroup等linux kernel功能的，因此container的guest系统只能是linux base的
隔离性相比KVM之类的虚拟化方案还是有些欠缺，所有container公用一部分的运行库
网络管理相对简单，主要是基于namespace隔离
Cgroup的cpu和cpuset提供的cpu功能相比KVM等的虚拟化方案相比难以度量（所以dotcloud主要是按内存收费）
Docker对disk和管理比较有限
Container随着用户进程的停止而销毁，container中的log等用户数据不便收集





# 进价篇

* Docker 数据卷

数据卷是一个可供一个或多个容器使用的特殊目录，它绕过UFS,可以提供很多用用的特性
数据卷可以在容器之间共享和重用
对数据卷的修改会立马生效
对数据卷的更新，不会影响镜像
卷会一直存而，直到没有容器使用
卷的使用，类似于Linux下对目录或文件进行mount
建立一个数据卷
创建一个web容器，并加载一个数据卷到容器的/webapp目录
Docker run –d –P –name web –v /webapp  training/webapp python ap.py
也可以在Dockerfile中使用VOLUME来添加一个或者多个新的卷到该镜像创建的任意容器
挂载一个主机目录作为数据卷
Docker run –d –P –name  web –v /src/webapp:/opt/webapp:ro(rw) training/webapp python app.py
加载主机的/src/webapp目录到容器的/opt/webapp目录
挂载一个本地主机文件作为数据卷
Docker run –rm –it –v ~/.bash_history:/.bash_history Ubuntu /bin/bash

创建一个命名的数据卷容器dbdata
Docker run –d –v /dbdata –name dbdata  training/postgres echo Data-only container
在其它容器中使用—volumes-from来挂载dbdata容器中的数据卷
Docker run –d –volumes-from dbdata –name db1 training/postgres
--volumes-from参数所挂载数据卷的容器自己并不需要保持而运行状态
Docker run –d –name db3 –volumes-from db1 training/postgress,也可以从其他已经挂载了数据卷的容器来挂载数据卷

利用数据卷容器来备份、恢复、迁移数据卷
备份
Docker run –volumes-from dbdata –v $(pwd):/backup Ubuntu tar cvf /backup/backup.tar
使用了tar命令将dbdata卷备份为本地的/backup/backup.tar
恢复
首先创建一个带有数据卷的容器dbdata2
docker run –v /dbdata  --name dbdata2  Ubuntu /bin/bash
然后创建另一个容器，挂载dbdata2的容器，并使用untar 解压备份文件到挂载的容器卷中
Docker run –volumes-from dbdata2 –v $(pwd):/backup busybox tar xvf /backup/backup.tar



* Docker 中的网络

Docker允许通过外部访问容器或容器互联的方式来提供网络服务
Ip:hostport:containerport |ip::containerPort |hostport:containerport
Docker run –d –p 127.0.0.1:5000:5000(/udp) training/webapp python app.py
容器有自己的内部网络和IP地址(docker inspect可以获取所有变量，-ip可以指定多个端口）
Docker inspect –f “{{ .Name }}” containerName,查看容器名字或其它信息
容器互联
--link name:alias,name是要链接容器的名称，alias是这个连接的别名，参可以让容器之间安全的进行交互
Docker run –d –name db training/postgres
Docker rm –f web
Docker run –d –P –name web –link db:db training/webapp python app.py
Docker通过2种方式为容器公开连接信息
环境变量
更新/etc/hosts文件
Docker run –rm –name web2 –link db:db training/webapp env
Docker run –t –I –rm –link db:db training/webapp /bin/bash , cat /etc/hosts


* Docker 中的网络配置

Docker启动时，会自动而主机上创建一个docker0虚拟网桥，实际上是Linux的一个bridge,可以理解为一个软件交换机，它会而挂载到它的网口之间进行转发
当创建一个Docker容器的时候，同理会创建一对veth pair接口(当数据包发送到一个接口时，另外一个接口也可以收到相同的数据包)，这对接口一端在容器内，即eth0;另一端在本地并被挂载到docker0网桥，名称以veth开头

Docker没有为每个容器专门定制镜像，通过虚拟文件来挂载到容器的3个相关配置mount
让宿主机DNS信息更新后，所有Docker容器的dns配置通过/etc/resolv.conf文件立刻得到更新
容器访问外部网络
通过iptables, sysctl –w net.ipv4.ip_forward=1,如果在启动Docker服务的时候设定—ip-forward=true,Docker就会自动设定系统的ip_forward的参数为1.
容器之间访问，需要两方面 的支持
容器的网络拓扑已经互联，默认情况下，所有容器都被连接到docker0网桥上
本地系统的防火墙软件 –iptables是否允许通过
容器访问外部实现
容器所有到外部的连接，源地址都会被NAT成本地系统的IP地址，这是使用iptables的源地址伪装操作实现的
Iptables –t nat –nL
外部访问容器，通过docker run时通过-p 或-P参数来启用
如果希望永久绑定到某个固定的iP地址，可以而Docker配置/etc/default/docker中指定DOCKER_PTS=“—ip=IP_ADDRESS”，之后重启DOCKER服务即可生效（http proxy, registry服务器地址指定，DOCKER服务参数修改）

配置docker0网桥
Docker run –I –t –rm Ubuntu /bin/bash
Ip addr show eth0, ip route
自定义网桥
先停止服务
Service docker stop
Ip link set dev docker0 down
Brctl del brdocker0
创建网桥
Brctl addbr bridge0
Ip addr add 192.168.5.1/24 dev bridge0
Ip link set dev bridge0 up
查看
Ip add show bridge0
编辑网络配置文件
Docker1.2.0开始支持在运迁中的容器里编辑/etc/hosts,/etc/hostname,/etc/resolve.conf文件，这些修改是临时的，只在运行的容器中保留，容器终止或重启后并不会被 保存下来，也不会被docker commit提交

默认情况下，Docker会将所有容器连接到由docker0提供的虚拟子网中，用户有时候需要两个容器之间可以直连通信，而不用通过主机网桥进行桥接，解决办法很简，创建一对peer接口，分别放到两个容器中，配置成点到点链路类型即可docker practice p67
使用supervisor来管理进程
Docker容器而启动的时候开启单个进程，但我们可以通过superviso的开启多个服务



* Docker 多机互联

主机A和主机B的网卡都连着物理交换机的同一个vlan 101,这样网桥一和网桥三就相当于在同一个物理网络中，而容器一、容器三、空口四也在同一个物理网络中了，他们之间可以相互通信，而且可以跟同一个vlan中的其他物理机器互联。需要自己保证容器的网络安全了。


* Docker 生态链介绍

Docker compose(把fig收购了)
Daocloud
Hujb2000/docker,
Docker build –t hujb2000/pm2 .
docker push hujb2000/pm2
Kubermetes
是Google团队发起并维护的基于Docker的开源容器集群管理系统，它不仅支持常规的云平台，而且支持内部数据中心。
Fig:在你的应用里添加一个fig.yml文件，并指定一些简单的内容，执行fig up它就能帮你快速 建立起一个容器，OSX和64位的Linux，是python语言写的。
使用Rail入门fig
CoreOS
CoreOS的设计是为你提供能够像谷歌一样的大型互联网公司一样的基础设施管理能力来动态扩展和管理的计算能力，CoreOS的安装文件和运行以来非常小，它提供了精简的Linux系统，它使用Linux容器在更高的抽象层来管理你的服务，而不是通过常规的YUM和APT来安装包


# Docker Ｃompose介绍
* Docker K8S介绍


# Docker实践篇

* 收集需求,了解项目
* PHP语言开发流程示例

1. 制作基础镜像
2. 编排开发运行环境
3. 打包并运行测试镜像
4. 发布生产镜像
5. 更新运行环境


* ＪAVA语言开发流程示例

1. 制作基础镜像
2. 编排开发运行环境
3. 打包并运行测试镜像
4. 发布生产镜像
5. 更新运行环境



删除容器和镜像
Docker rm ${docker ps –a –q} #删除所有容器Docker rm $(docker ps –a –q)
Docker rm <容器名 煌ID> #删除单个容器
Docker rmi <ID> #删除单个镜像
Docker rmi $( docker images | grep “<none>”| awk ‘{print $3}’ | sort –r ) #删除所有镜像
启动停止容器
Docker stop (容器名 or ID) #停止某个容器
Docker start (容器名 or ID) #启动某个容器
Docker kill (容器名 or ID) #杀掉某个容器
容器迁移
Docker exort <container id>  > /home/export.tar  #导出
Cat /home/export.tar | sudo docker import – busybox-1-export:latest #导入export.tar文件
Docker save debian > /home/save.tar #将debian容器打包
Docker load < /home/save.tar #在另一台服务器上加载打包文件
运行一个新容器
#运行一个新窗口，同时为它命名、端口映射。以debian02镜像为例
Docker run –h=“redis-test”  --name  redis-test  -d –p 51000:22 –p 51001:3306  -p  510003:6379
#从container中拷贝文件，当container已经关闭后，在里面的文件还可以拷贝出来。
Sudo docker cp <container id> :/etc/debian_version .  #把容器中的/etc/debian_version拷贝到当前目录下


Docker run [options] image[:tag] [command] [args…]
CONTAINER_ID=$(docker run –d Ubuntu /bin/sh –c “while true;do echo hello world; sleep 1; done”)
Docker logs $CONTAINER_ID
Docker attach –sig-proxy=false $CONTAINER_ID，允许我们查看一个 后台进程
Docker stop $CONTAINER_ID


docker images -q | xargs docker rmi -f    删除所有image, (-f 强制删除，有运行也删除)
docker rmi -f $(docker images | grep “<none>” | awk “{print \$3}”)，删除none镜像

Docker run –t b15 yum install –y wget, 每次执行docker run都会独立的创建一个新的container来执行程序，所以我们必须手动把对这些container的更改提交成一个新的image，才能够依据这个image来执行wget操作
Docker run –t –I b15 /bin/bash
Yum install –y wget
Docker ps –a
Docker commit 26(containerid前几位)  new_image_name
Docker run –t –I –rm=true new_image_id  wget http://www.baidu.com

从container往host拷贝文件
Docker cp <container_id>:/root/hello.txt .
从host往container里拷贝文件，
首先停止container(当然不停止也能拷贝) docker stop <container_name_or_id>
Cp /tmp/tmp.txt   /var/lib/docker/aufs/mnt/<ContainerID>/tmp?
如果我想要进入一个运行中的docker container ，可以使用docker attach,连上     	这个container的输入和输出
文件卷加载
挂载主机的文件卷Docker run –rm=true –I –t –name=ls-volume –v /etc/:/opt/etc/ centos
-v  /etc:/opt/etc/:ro #read only
挂载其它container中的文件系统，需要用到—volume-from能数
Docker run –d –I –t –p 1337:1337 –name nodedev –v /var/ fa node  /var/nodejs/app.js(先创建一个container，他共享/var/目录给其他container)
Docker run –rm=true –I –t –volumes-from nodedev –name=aaa centos ls /var

发布到docker hujb上
Docker long
Docker push <用户名>/<镜像名>
Docker inspect  <containerId | imageID>返回容器或镜像底层信息
Docker events 从服务器获取实时事件，监听事件
Docker events –since 1378216169
Docker history image
列出全部镜像的ID, docker images –notrunc | head
Docker info
Docker insert IMAGE URL PATH,通过url给镜像路径增加文件
Docker logs [options] CONTAINER 取出容器的log日志
Docker port [OPTIONS] CONTAINER PRIVATE PORT查看私有地址转换到公有地址端口


# Docker OSChina.net

docker run --name='gitlab' -it --rm \
-e 'GITLAB_PORT=10080' -e 'GITLAB_SSH_PORT=10022' \
-p 10022:22 -p 10080:80 \
-v /var/run/docker.sock:/run/docker.sock \
-v $(which docker):/bin/docker \
sameersbn/gitlab:latest

然后打开浏览器访问 http://localhost:10080，用户名密码如下：

username: root
password: 5iveL!fe


# Heroku Platform

[Heroku](https://www.heroku.com/platform)

Deploy and run apps on today's most innovative Platform as a Service

The Heroku  Platform is a cloud platfrom based on a managed container system, with integrated data services and a powerful ecosystem. for deploying and running modern apps . The Heroku developer experience is an app centric approach for software delivery, integrated with today's most popular developer tools and workflows.


* Heroku Postgress

The SQL database service for developers

Operation Expertise, Built In

Access your data anywehre, scale without worry.

Heroku  Postgres provides a SQL database-as-a-service that lets you focus on building your application instead of messing around with database management.


*  Heroku Redis

* Heroku CLI

The Heroku CLI is used to manage Heroku apps from the command line. ruby language written.


# Flocker

Flocker is an open-source Container Data Volume Manager for your Dockerized application. written by python languange.


# 基于Docker开发的Pass平台DINP, Go语言编写,有个用Java

# docker-registry-driver-qiniu

Docker registry 的七牛驱动

通过Docker hub可以直接安装运行：

docker run --rm \
  -e SETTINGS_FLAVOR=qiniustorage \
  -e QINIU_BUCKET=YOUR_BUCKET \
  -e QINIU_ACCESSKEY=YOUR_ACCESSKEY \
  -e QINIU_SECRETKEY=YOUR_SECRETKEY \
  -e QINIU_DOMAIN=YOUR_BUCKET_DOMAIN \
  -p 5000:5000 \
  --name registry \
  zhangpeihao/docker-registry-qiniu


This is a docker-registry backend driver for Qiniu Cloud Storage.

# 基于Docker的操作系统RancherOS
 [RancherOS](http://rancher.com/rancher-os/?from=groupmessage&isappinstalled=0)

 The perfect little place to run Docker, RancherOS is a 20mb Linux distro taht runs the entire OS as Docker containers.

 # Docker 可视化管理Panamax

 Panamax 是一个开源的项目，可以通过简单的拖拉操作就可以实现发布复杂的 Docker 容器应用。Panamax 为 Docker, Fleet & CoreOS 提供友好的管理界面。
 容器技术是下一代的虚拟机，但使用该技术运行多容器、多服务器应用是非常困难的。你必须学习 5 种不同技术和最佳实践，包括：libswarm, systemd, etcd, ambassadord, fleet, 等等。而 Panamax 帮你集成了这些 Docker 的最佳实践，并提供了一个体验良好的可视化界面来发布复杂应用。

 [Panamax](http://panamax.io/)


# Docker管理工具 Shipyard

Shipyard 是一个基于 Web 的 Docker 管理工具，支持多 host，可以把多个 Docker host 上的 containers 统一管理；可以查看 images，甚至 build images；并提供 RESTful API 等等。 Shipyard 要管理和控制 Docker host 的话需要先修改 Docker host 上的默认配置使其支持远程管理。


Go语言编写

# Docker注册表的前端和授权工具Portus

Portus 是用于 Docker RegistryAPI（v2）的开源前端和授权工具，最低要求注册表版本是 2.1。它可以作为授权服务器和用户界面，用于新一代的 Docker Registry。

安全。Portus 实现了最新的 Docker Registry中定义的新的授权方案。它允许对你所有的镜像进行细颗粒度控制，你可以决定哪个用户和团队可 push／pull 镜像。

轻松管理用户。 在 Portus 映射你的公司，可以定义任意数量的 team，并从 team 添加和移除用户。Team 有三种类型的用户：Viewers ，只能 pull 镜像；Contributors，可以 push ／ pull 镜像；Owners，类似 contributors，但可以从 team 添加或移除用户。

搜索。Portus 提供你的私人注册表的内容的预览，同时有一个快速搜索镜像的功能。

Audit。所有相关事件都会被 Portus 自动记录，可被管理员用户分析。

Ruby written by ruby

[Portus](https://github.com/SUSE/Portus)

# Docker 远程代理Ａｍｂassadord

Ambassadord是 Docker 远程代理（Ambassador）模式的实现，它允许跨主机连接Docker容器，支持静态转发、基于DNS的转发或者基于Consul+Etcd的转发。通过使用iptables，Ambassadord可以基于端口来选择跳转到哪个主机，因此，集群中只需要一个代理即可。

Go ｗritte

# Docker的管理工具 UI DockerUI

Docker UI 是 Docker的基于Web的管理UI


[Docker UI](https://github.com/crosbymichael/dockerui)



# 基于Docker的PaaS系统 Dawn

Dawn 是一个基于 Docker 的 PaaS 系统，使用 Ruby 开发。实现了类 Heroku 的接口。该项目是在 2013年10月 开始的，原本计划是作为商业服务发布，但由于 PaaS 市场的竞争越来越激烈，因此决定开源。

当前开发的版本是基于 Ubuntu 14.04，运行了 docker, ruby 2.1.2 (rails 4.1.1), postgresql, redis, logplex 和 hipache.

将来的目标是将平台移植到 CoreOS 上，并将应用放置到不同的容器上，以便更加模块化，同时更加容易发布。

特性：

通过 Git 将应用发布到平台
使用 Buildstep 构建应用容器
可导入环境变量到应用空间
可通过 HTTP POST 来获取应用日志
per-proctype 实现伸缩
要求

支持 AMD64 虚拟机
Vagrant >= 1.6.2
Ansible >= 1.6.2
耐心

flynn  instead

ruby written


# CoreOS的IaaＳ/Docker编配平台Stampede

Stampede 是基于 CoreOS 的混合 IaaS/Docker 编配平台。Stampede 需要一个空的 CoreOS 集群，通过简单的配置就可以拥有可以同时运虚拟机和 Docker 的平台。Stampede 能很好的支持 IaaS 到 Docker 的复杂业务流程，增强了网络，存储和管理方面的能力。Stampede 的最终目标是继续支持传统的 IaaS，同时增强对 Docker 和容器的支持。

rancher stead.

# 容器集群管理系统 Kubernetes

Kubernetes 是来自 Google 云平台的开源容器集群管理系统。基于 Docker 构建一个容器的调度服务。该系统可以自动在一个容器集群中选择一个工作容器供使用。其核心概念是 Container Pod。详细的设计思路请参考这里。

# 在线代码运行平台

glot 是可以可以在线运行各种编程语言代码片段的平台，包含如下组件：

glot-www - glot.io website
glot-snippets - snippets api
glot-run - code runner api
glot-code-runner - code runner tool
glot-containers - docker containers
项目采用 Haskell Script 、Go、Erlang 和 Shell 开发，运行环境基于 Docker 容器进行。

[glot](https://glot.io/)

# CoreOS的容器引擎

Rocket （也叫 rkt）是 CoreOS 推出的一款容器引擎，和 Docker 类似，帮助开发者打包应用和依赖包到可移植容器中，简化搭环境等部署工作。Rocket 和 Docker 不同的地方在于，Rocket 没有 Docker 那些为企业用户提供的“友好功能”，比如云服务加速工具、集群系统等。反过来说，Rocket 想做的，是一个更纯粹的业界标准。

CoreOS 把它的容器称为 App Containers，里面包含 app container image、runtime、container-discovery 协议等。其中，App Container Image 和 Docker 里的 Image 比较类似，包含应用必需的元素组成，如源代码和二进制文件。Rocket runtime 则是依照 App Container 标准规格打造的，旨在将容器真正的变成一款命令行工具。

[rocket](https://github.com/coreos/rkt)

# 开源PaaS系统Deis

Deis 是一个 Django/Celery API 服务器、Python CLI 和一组 Chef cookbooks 合并起来提供一个类似 Heroku 的应用平台，用于公有云和私有云。Deis 的口号是：Your PaaS. Your Rules.

Deis 是一个开源的 PaaS 系统，简化和 LXC 容器和 Chef 节点的发布和伸缩。可用于托管应用、数据库、中间件和其他服务。Deis 利用 Chef、Docker 和 Heroku Buildpacks 来提供的私有 PaaS 是非常轻量级和灵活的。

Deis 提供开箱即用的 Ruby, Python, Node.js, Java, Clojure, Scala, Play, PHP, Perl, Dart 和 Go 语言的支持。此外 Deis 可使用 Heroku Buildpacks、Docker images 和 Chef recipes 发布任何内容。Deis 主要设计用来跟不同的云提供商进行交互，支持 EC2 等平台。

[Deis](http://deis.io/)

# Web 安全扫描平台 Gryffin

Gryffin 是雅虎开发的一个大规模 Web 安全扫描平台。它不是另外一个扫描器，其主要目的是为了解决两个特定的问题 —— 覆盖率和伸缩性。

该平台采用 Go 语言开发，依赖

# 集群管理系统Photon Controller

[Photon Controller](http://www.oschina.net/p/photon-controller)

# 开源看板管理系统LibreBoard

LibreBoard 是一个卡片式的组织 Kanban 的开源实现。可以用来实现团队内部的协作沟通，你可以吧 LibreBoard 看成是 Trello 的开源版本。

看板管理，常作“Kanban管理”（来自日语“看板”，カンバン，日语罗马拼写：Kanban），是丰田生产模式中的重要概念，指为了达到及时生产（JIT）方式控制现场生产流程的工具。及时生产方式中的拉式（Pull）生产系统可以使信息的流程缩短，并配合定量、固定装货容器等方式，而使生产过程中的物料流动顺畅。

[LibreBoard](http://try.wekan.io/) 为 Sandstorm 平台提供了一键安装以及一个经过验证的 Docker 映像。

# Paas平台Peas

Peas = PaaS for the People

Peas 是一个 Heroku 风格的 PaaS 平台，使用 Ruby 开发，基于 Docker 平台。其灵感来自于 Deis 和 Dokku.
Peas 的理念是可轻松访问以及易于调整，它并非想作为完整的企业解决方案，而是一个相对要简单，但基于良好基础的系统，包括：Ruby;Rspec,Bundler,Guard,Rack,Puma,Grape,Sidekiq,GLI 等等

https://github.com/tombh/peas

#  开源应用容器Kontena

Kontena 是采用 Ruby 开发的应用容器，是一个开源的容器化业务流程工具，提供云基础设施上容器化应用的部署、管理、测量和监控工具。

Kontena 包括 Server，Client 和 CLI 三个部分，支持任意的云平台，比如 Docker 和 CoreOS Rocket。

Kontena 通常使用命令来操作：

[Kontena](http://www.kontena.io/)

[codepicnic](https://codepicnic.com/)

# 持续部署产品环境Paz

Paz 是一个基于 Docker、CoreOS、etcd 和 fleet 的持续部署产品环境。是一个类似 PaaS 工作流程的可插入式服务平台。Paz 使用 Node.js 编写。

[Paz](http://www.paz.sh/)

# ｖagrant-mesos

vagrant-mesos 是一款运维工具，可以使 Mesos 集群的安装和运行更加容易。

vagrant-mesos 支持 Mesos 0.21.0 集群，同时包括 Marathon (0.8.0) 和 Chronos (2.1.0)正在运行的框架服务器节点。这意味着，你可以使用 vagrant up，打造自己的 Mesos+Marathon+Chronos+Docker PaaS 平台。Marathon 作为 分布式 init.d， Chronos 作为分布式 cron。


# Gogs

Gogs(Go Git Service) 是一款极易搭建的自助Git托管服务

# Drone-CI

Drone 是一个建立在 Docker 之上的 持续集成(Continuous integration)系统。官方支持下面的系统和版本：

Ubuntu Precise 12.04 (LTS) (64-bit)
Ubuntu Raring 13.04 (64 bit)
Drone 的安装仅仅依赖最新版本的 Docker(0.8)，所以安装它前你需要确保 Docker 已安装。

Written in Go

# 持续集成客户端JoliCI

JoliCi 是一个免费的开源的持续集成客户端，它由 PHP 写成，支持 Docker。它用来与现有的 Ci 服务兼容，如 Travis-Ci，而且不会创建新的标准。


[JoliCI](https://github.com/jolicode/JoliCi)




[Gogs](http://git.oschina.net/Unknown/gogs)
