---
layout: post
title:  "Docker Training's Outline"
date:   2015-12-01 13:35:30
categories: allen.hu update
---



# Docker基础篇

	## Docker简介

		### 什么是Docker
		### Docker技术的催生条件
		### 为什么用Docker

		    #### Docker的优势
			#### Docker与VM对比
			#### Docker与其它容器对比

	## Docker的意义

		### Docker对开发流程的再造


	## Docker基本概念

		### Docker Client
		### Docker Daemon
		### Docker Hub/Docker Registry/Docker private Registry
		### Docker 镜像
		### Docker 容器

			#### 容器原理
			#### 容器的隔离性
			#### cgroups
			#### Docker 分层存储(AUFS)

	## Docker常用命令

		### 安装
		### 拉取镜像
		### 给镜像打TAG
		### 提交镜像
		### PUSH镜像
		### 运行镜像

			#### -p与-P参数
			#### --env参数
			#### -v 参数
			#### -entrypoint参数
			#### --name参数
			#### --link参数
			....


	## Dockerfile制作原则与规则

# 进价篇

	## Docker 数据卷
	## Docker 中的网络
	## Docker 中的网络配置
	## Docker 多机互联
	## Docker 生态链介绍

		### Docker Compose介绍
		### Docker K8S介绍
		### CoreOS 介绍
		...


# Docker实践篇

	## Docker最佳实践-全栈开发介绍
	## 最佳实践案例-PHP语言版

		### 收集需求,了解项目
		### PHP语言开发流程示例

			1. 制作基础镜像
			2. 编排开发运行环境
			3. 打包并运行测试镜像
			4. 发布生产镜像
			5. 更新运行环境


	## 最佳实践案例-JAVA语言版

		### 收集需求,了解项目
		### JAVA语言开发流程示例

			1. 制作基础镜像
			2. 编排开发运行环境
			3. 打包并运行测试镜像
			4. 发布生产镜像
			5. 更新运行环境
