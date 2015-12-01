---
layout: post
title:  "Docker Training"
date:   2015-12-01 13:35:30
categories: allen.hu update
---


docker介绍与入门
1.什么是D
2.示例

docker原理
1.原理
2.docker file解析
3.更深入的示例


docker 实战
1.开发应用
2.测试持续集成
3.部署运维

docker高级特性
1.环境变量，目录,网络模式
2.多镜像协作，编排


大纲略挫。。。
把一堆概念放在高级特性我觉得不合适， 应该从怎样使用docker为开发流程服务的角度， 把知识点串在里面


看看希云的，知识点分的比较完整了，但还是缺乏对怎样实践docker的指导。
https://csphere.cn/training


 # 培训大纲

 ## Docker实践之入门以及Dockerfile

 1. 基本概念
 2. 常用命令
 3. Dockerfile的编写
 4. 构建Docker镜像的(4个经典案例)
 5. 使用Docker部署Wordpress用例

 ## Docker实践之Registry以及持续集成

 1. 搭建私有DockerHub
 2. 自动构建Docker镜像
 3. 通过compose一键部署多个容器
 4. Jenkins与 Docker配合做持续集成
 5. 通过Docker自动集成测试


 ## Docker实践之监控报警以及日志管理

 1. 搭建监控报警系统
 2. 搭建日志管理系统
 3. 模拟访问场景(产生压力)
 4. 收集日志,并图表化展现
 5. 通过普罗米修斯数据库做docker监控，通过ELK做日子收集和展现

 ## Docker实践之网络管理

 1. 熟悉Docker网络模式:nat\host\container\none\overlay 5 种网络
 2. 了解网络模式的特点和使用场景
 3. 使用Docker1.8 experiment版本实现跨越主机通信

 ## Docker实践之持续部署以及弹性 伸缩

 1. 搭建swarm集群,并演示如何与compose结合
 2. 通过compose自动部署应用,并进行扩容缩容

 ## Docker实践之存储

 1. 了解Docker Graph存储，包括aufs、devicemapper、overlayfs，掌握每种存储的使用方法，优缺点，以及我们如何选择
 2. 学习Docker如何运行数据类服务，如何用好Volume





# Docker基础篇
## Docker简介
## Docker与VM对比
## Docker对开发流程的再造
## Docker基本概念
	* Docker 命令行
	* Docker Daemon
	* Docker Hub/Docker Registry/Docker private Registry
	* Docker 镜像
	* Docker 容器
	* Docker 分层存储(AUF)
## Docker常用命令
	* 安装
	* 拉取镜像
	* 给镜像打TAG
	* 提交镜像
	* PUSH镜像
	* 运行镜像
## Dockerfile制作原则与规则

# Docker中级篇

	* Docker 数据卷
	* Docker 中的网络
	* Docker 中的网络配置
	* Docker 多机互联


# Docker高级篇

	* Docker 生态链介绍
	* Docker compose介绍
	* Docker K8S介绍
	* Docker MongoDB集群搭建
	* Docker Redis Sentinal模式搭建
	* Docker RabbitMQ集群搭建
	* Docker MySQL集群搭建
	* Docker Hadoop集群搭建


# Docker实践篇

	* 收集需求,了解项目
	* 制作基础镜像
	* 编制Docker.compile文件编排开发运行环境
	* 拉取EasyNode样片工程
	* 开发Demo
	* 打包镜像并Launch镜像给ＱＡ测试
	* 发布
	* 更新运行环境
	* 不停服扩容
	* 不停服升级应用
	* 不停服回滚
