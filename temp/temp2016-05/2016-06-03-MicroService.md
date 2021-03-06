---
layout: post
title:  "Micro Service"
date:   2016-06-03 13:35:30
categories: allen.hu update
---

#  Micro Service

[微服务](http://www.jianshu.com/p/c63a739914bf)

## 微服务架构的优势与不足

Monolithic

1. 体积大，启动时间长，不利于持续性开发

这种微服务架构模式深刻影响了应用和数据库之间的关系，不像传统多个服务共享一个数据库，微服务架构每个服务都有自己的数据库。


微服务架构的好处

微服务的目的是有效的拆分应用，实现敏捷开发和部署。

1. 微服务架构模式有很多好处。首先，通过分解巨大单体式应用为多个服务方法解决了复杂性问题。在功能不变的情况下，应用被分解为多个可管理的分支或服务。每个服务都有一个用RPC-或者消息驱动API定义清楚的边界。微服务架构模式给采用单体式编码方式很难实现的功能提供了模块化的解决方案，由此，单个服务很容易开发、理解和维护。

2. 这种架构使得每个服务都可以有专门开发团队来开发。开发者可以自由选择开发技术，提供API服务。

3. 第三，微服务架构模式是每个微服务独立的部署。开发者不再需要协调其它服务部署对本服务的影响。这种改变可以加快部署速度。UI团队可以采用AB测试，快速的部署变化。微服务架构模式使得持续化部署成为可能。

4. 微服务架构模式使得每个服务独立扩展。你可以根据每个服务的规模来部署满足需求的规模。甚至于，你可以使用更适合于服务资源需求的硬件。比如，你可以在EC2 Compute Optimized instances上部署CPU敏感的服务，而在EC2 memory-optimized instances上部署内存数据库。


微服务的不足

1. 微服务应用是分布式系统，由此会带来固有的复杂性。
2. 微服务的挑战来自于分区的数据库架构，一系列存储服务调用和消息中间件调用的CAP一致性
3. 服务架构模式就需要考虑相关改变对不同服务的影响。
4. 部署一个微服务应用也很复杂，成功部署一个微服务应用需要开发者有足够的控制部署方法，并高度自动化。
PaaS给开发者提供一个部署和管理微服务的简单方法，它把所有这些问题都打包内置解决了。
这就造成许多需要配置、部署、扩展和监控的部分

构建复杂的应用真的是非常困难。单体式的架构更适合轻量级的简单应用。如果你用它来开发复杂应用，那真的会很糟糕。微服务架构模式可以用来构建复杂应用，当然，这种架构模型也有自己的缺点和挑战。

在后续的博客中，我会深入探索微服务架构模式，并讨论诸如服务发现、服务部署选择和如何分解一个分布式应用为多个服务的策略。

## 构建微服务：使用API GATEWAY

1. 客户端直接与服务器端通信的方式很少在实际中使用。

2. API Gateway.如授权、监控、负载均衡、缓存、请求分片和管理、静态响应处理等,API Gateway负责请求转发、合成和协议转换。所有来自客户端的请求都要先经过API Gateway，然后路由这些请求到对应的微服务。API Gateway将经常通过调用多个微服务来处理一个请求以及聚合多个服务的结果。它可以在web协议与内部使用的非Web友好型协议间进行转换，如HTTP协议、WebSocket协议

API Gateway可以提供给客户端一个定制化的API。它暴露一个粗粒度API给移动客户端,一个适配器处理一个请求平均要调用6到8个后端服务。

* API Gateway的优点与缺点

API Gateway的一个最大好处是封装应用内部结构。相比起来调用指定的服务，客户端直接跟gatway交互更简单点。API Gateway提供给每一个客户端一个特定API，这样减少了客户端与服务器端的通信次数，也简化了客户端代码。

API Gateway也有一些缺点。它是一个高可用的组件，必须要开发、部署和管理。还有一个问题，它可能成为开发的一个瓶颈。开发者必须更新API Gateway来提供新服务提供点来支持新暴露的微服务。更新API Gateway时必须越轻量级越好。否则，开发者将因为更新Gateway而排队列。但是，除了这些缺点，对于大部分的应用，采用API Gateway的方式都是有效的。

性能和可扩展性

只有少数公司需要处理像Netflix那样的规模，每天需要处理数十亿的请求。但是，对于大多数应用，API Gateway的性能和可扩展性也是非常重要的。因此，创建一个支持同步、非阻塞I/O的API Gateway是有意义的。已经有不同的技术可以用来实现一个可扩展的API Gateway。在JVM上，采用基于NIO技术的框架，如Netty，Vertx，Spring Reactor或者JBoss Undertow。Node.js是一个非JVM的流行平台，它是一个在Chrome的JavaScript引擎基础上建立的平台。一个可选的方案是NGINX Plus。NGINX Plus提供一个成熟的、可扩展的、高性能web服务器和反向代理，它们均容易部署、配置和二次开发。NGINX Plus可以管理授权、权限控制、负载均衡、缓存并提供应用健康检查和监控。

采用反应性编程模型

利用传统的同步回调方法来实现API合并的代码会使得你进入回调函数的噩梦中。这种代码将非常难度且难以维护。一个优雅的解决方案是采用反应性编程模式来实现。类似的反应抽象实现有Scala的Future，Java8的CompletableFuture和JavaScript的Promise。基于微软.Net平台的有Reactive Extensions(Rx)。Netflix为JVM环境创建了RxJava来使用他们的API Gateway。同样地，JavaScript平台有RxJS，可以在浏览器和Node.js平台上运行。采用反应编程方法可以帮助快速实现一个高效的API Gateway代码。

* 服务调用

一个基于微服务的应用是一个分布式系统，并且必须采用线程间通信的机制。有两种线程间通信的方法。一种是采用同步机制，基于消息的方法。这类的实现方法有JMS和AMQP。另外的，例如Zeromq属于服务间直接通信。还有一种线程间通信采用异步机制，例如Thrift和HTTP。事实上一个系统会同时采用同步和异步两种机制。由于它的实现方式有很多种，因此API Gateway就需要支持多种通信方式。

API Gateway需要采用系统的服务发现机制，要么采用服务端发现，要么是客户端发现。

##  深入微服务架构的进程间通讯

在单体式应用中，各个模块之间的调用是通过编程语言级别的方法或者函数来实现的。但是一个基于微服务的分布式应用是运行在多台机器上的。一般来说，每个服务实例都是一个进程。因此，如下图所示，服务之间的交互必须通过进程间通信（IPC）来实现。


一种解决方案是把版本号嵌入到URL中。每个服务都可能同时处理多个版本的API。或者，你可以部署多个实例，每个实例负责处理一个版本的请求。

• 网络超时：当等待响应时，不要无限期的阻塞，而是采用超时策略。使用超时策略可以确保资源不会无限期的占用。
• 限制请求的次数：可以为客户端对某特定服务的请求设置一个访问上限。如果请求已达上限，就要立刻终止请求服务。
• 断路器模式（Circuit Breaker Pattern）：记录成功和失败请求的数量。如果失效率超过一个阈值，触发断路器使得后续的请求立刻失败。如果大量的请求失败，就可能是这个服务不可用，再发请求也无意义。在一个失效期后，客户端可以再试，如果成功，关闭此断路器。
• 提供回滚：当一个请求失败后可以进行回滚逻辑。例如，返回缓存数据或者一个系统默认值。


有很多消息系统可以选择，最好选择一种支持多编程语言的。一些消息系统支持标准协议，例如AMQP和STOMP。其他消息系统则使用独有的协议，有大量开源消息系统可选，比如RabbitMQ、Apache Kafka、Apache ActiveMQ和NSQ。它们都支持某种形式的消息和channel，并且都是可靠的、高性能和可扩展的；然而，它们的消息模型完全不同。

开发者社区最近重新发现了RESTful API接口定义语言的价值。于是就有了一些RESTful风格的服务框架，包括RAML和Swagger。一些IDL，例如Swagger允许定义请求和响应消息的格式。其它的，例如RAML，需要使用另外的标识，例如JSON Schema。对于描述API，IDL一般都有工具来定义客户端和服务端骨架接口。


* Thrift

Apache Thrift是一个很有趣的REST的替代品。它是Facebook实现的一种高效的、支持多种编程语言的远程服务调用的框架。Thrift提供了一个C风格的IDL定义API。使用Thrift编译器可以生成客户端和服务器端代码框架。编译器可以生成多种语言的代码，包括C++、Java、Python、PHP、Ruby, Erlang和Node.js。

## 服务发现的可行方案以及实践案例


目前有两大类服务发现模式：客户端发现和服务端发现。

我们先来来讨论一下客户端发现。

*   客户端服务发现

Netflix OSS提供了一种非常棒的客户端发现模式。Netflix Eureka是一个服务注册表，为服务实例注册管理和查询可用实例提供了REST API接口。Netflix Ribbon是一种IPC客户端，与Eureka合同工作实现对请求的负载均衡。我们会在后面详细讨论Eureka。

客户端发现模式也是优缺点分明。这种模式相对比较直接，而且除了服务注册表，没有其它改变的因素。除此之外，因为客户端知道可用服务注册表信息，因此客户端可以通过使用哈希一致性（hashing consistently）变得更加聪明，更加有效的负载均衡。

而这种模式一个最大的缺点是需要针对不同的编程语言注册不同的服务，在客户端需要为每种语言开发不同的服务发现逻辑。

* 服务器端服务发现

TTP服务和类似NGINX和NGINX Plus的负载均衡器都可以作为服务端发现均衡器。例如，这篇博文（https://www.airpair.com/scalable-architecture-with-docker-consul-and-nginx）就描述如何使用Consul Template来动态配置NGINX反向代理。Consul Template是周期性从存放在Consul Template注册表中配置数据重建配置文件的工具。

当文件发生变化时，会运行一个命令。在如上博客中，Consul Template产生了一个nginx.conf文件，用于配置反向代理，然后运行一个命令，告诉NGINX重新调入配置文件。更复杂的例子可以用HTTP API或者DNS动态重新配置NGINX Plus。

另外一些服务注册表例子包括：

etcd – 是一个高可用，分布式的，一致性的，键值表，用于共享配置和服务发现。两个著名案例包括Kubernetes和Cloud Foundry。

consul – 是一个用于发现和配置的服务。提供了一个API允许客户端注册和发现服务。Consul可以用于健康检查来判断服务可用性。

Apache ZooKeeper – 是一个广泛使用，为分布式应用提供高性能整合的服务。Apache ZooKeeper最初是Hadoop的子项目，现在已经变成顶级项目。

一个服务管理器的例子是开源项目Registrator，负责自动注册和注销被部署为Docker容器的服务实例。Reistrator支持多种服务管理器，包括etcd和Consul。

另外一个服务管理器例子是NetflixOSS Prana，主要面向非JVM语言开发的服务，也称为附带应用（sidecar application），Prana使用Netflix Eureka注册和注销服务实例。

服务管理器是部署环境内置的模块。有自动扩充组创建的EC2实例可以自向ELB自动注册，Kubernetes服务自动注册并且对发现服务可用。



## 微服务的事件驱动数据管理

获得原子性的一个方法是对发布事件应用采用multi-step process involving only local transactions，技巧在于一个EVENT表，此表在存储业务实体数据库中起到消息列表功能。应用发起一个（本地）数据库交易，更新业务实体状态，向EVENT表中插入一个事件，然后提交此次交易。另外一个独立应用进程或者线程查询此EVENT表，向消息代理发布事件，然后使用本地交易标志此事件为已发布，如下图所示：


此方法的例子如LinkedIn Databus 项目，Databus 挖掘Oracle交易日志，根据变化发布事件，LinkedIn使用Databus来保证系统内各记录之间的一致性。

另外的例子如：AWS的 streams mechanism in AWS DynamoDB，是一个可管理的NoSQL数据库，一个DynamoDB流是由过去24小时对数据库表基于时序的变化（创建，更新和删除操作），应用可以从流中读取这些变化，然后以事件方式发布这些变化。

## 选择微服务部署微略

一个微服务应用由上百个服务构成，服务可以采用不同语言和框架分别写就。每个服务都是一个单一应用，可以有自己的部署、资源、扩展和监控需求。例如，可以根据服务需求运行若干个服务实例，除此之外，每个实例必须有自己的CPU，内存和I/O资源。尽管很复杂，但是更挑战的是服务部署必须快速、可靠和性价比高。


服务可以用不同语言和框架写成，因此开发团队肯定有很多需要跟运维团队沟通事项。


单容器单服务实例模式

当使用这种模式时，每个服务实例都运行在各自容器中。容器是运行在操作系统层面的虚拟化机制。一个容器包含若干运行在沙箱中的进程。从进程角度来看，他们有各自的命名空间和根文件系统；可以限制容器的内存和CPU资源。某些容器还具有I/O限制，这类容器技术包括Docker和Solaris Zones。


然而，跟虚机不一样，容器是一个轻量级技术。容器映像创建起来很快，例如，在笔记本电脑上，将Spring Boot 应用打包成容器映像只需要5秒钟。因为不需要操作系统启动机制，容器启动也很快。当容器启动时，后台服务就启动了。

使用容器也有一些缺点。尽管容器架构发展迅速，但是还是不如虚机架构成熟。而且由于容器之间共享host OS内核因此并不像虚机那么安全。

* Serverless 部署

AWS Lambda是serverless部署技术的例子，支持Java，Node.js和Python服务；需要将服务打包成ZIP文件上载到AWS Lambda就可以部署。可以提供元数据，提供处理服务请求函数的名字（一个事件）。AWS Lambda自动运行处理请求足够多的微服务，然而只根据运行时间和消耗内存量来计费。当然细节决定成败，AWS Lambda也有限制。但是大家都不需要担心服务器，虚拟机或者容器内的任何方面绝对吸引人。

Lambda 函数 是无状态服务。一般通过激活AWS服务处理请求。例如，当映像上载到S3 bucket激活Lambda函数后，就可以在DynamoDB映像表中插入一个条目，给Kinesis流发布一条消息，触发映像处理动作。Lambda函数也可以通过第三方web服务激活。


部署微服务应用也是一种挑战。用各种语言和框架写成的服务成百上千。每种服务都是一种迷你应用，有自己独特的部署、资源、扩充和监控需求。有若干种微服务部署模式，包括单虚机单实例以及单容器单实例。另外可选模式还有AWS Lambda，一种serverless方法。

## 从单体式架构迁移到微服务架构

Martin Fowler将这种现代化策略成为绞杀（Strangler）应用，名字来源于雨林中的绞杀藤（strangler vine），也叫绞杀榕(strangler fig)。绞杀藤为了爬到森林顶端都要缠绕着大叔生长，一段时间后，树死了，留下树形藤。这种应用也使用同一种模式，围绕着传统应用开发了新型微服务应用，传统应用会渐渐退出舞台。

策略2——将前端和后端分离

减小单体式应用复杂度的策略是讲表现层和业务逻辑、数据访问层分开。典型的企业应用至少有三个不同元素构成：

表现层——处理HTTP请求，要么响应一个RESTAPI请求，要么是提供一个基于HTML的图形接口。对于一个复杂用户接口应用，表现层经常是代码重要的部分。

业务逻辑层——完成业务逻辑的应用核心。

数据访问层——访问基础元素，例如数据库和消息代理。

策略3——抽出服务

第三种迁移策略就是从单体应用中抽取出某些模块成为独立微服务。每当抽取一个模块变成微服务，单体应用就变简单一些；一旦转换足够多的模块，单体应用本身已经不成为问题了，要么消失了，要么简单到成为一个服务


将资源消耗大户先抽取出来也是排序标准之一。例如，将内存数据库抽取出来成为一个微服务会非常有用，可以将其部署在大内存主机上。同样的，将对计算资源很敏感的算法应用抽取出来也是非常有益的，这种服务可以被部署在有很多CPU的主机上。通过将资源消耗模块转换成微服务，可以使得应用易于扩展。

如何抽取模块

抽取模块第一步就是定义好模块和单体应用之间粗粒度接口，由于单体应用需要微服务的数据，反之亦然，因此更像是一个双向API。因为必须在负责依赖关系和细粒度接口模式之间做好平衡，因此开发这种API很有挑战性，尤其对使用域模型模式的业务逻辑层来说更具有挑战，因此经常需要改变代码来解决依赖性问题

# Build Microservice

http://www.dropwizard.io/0.9.2/docs/

https://github.com/Netflix/karyon

https://github.com/Netflix/Hystrix



