---
layout: post
title:  "Build Hadoop Cluster Based on Docker"
date:   2015-11-24 13:35:30
categories: allen.hu update
---


# Hadoop Project

	It is designed to scale up from single servers to thousands of machines, each offering local computation and storage. Rather than rely on hardware to deliver high-availability.

	the library itself is designed to detect and handle failures at the application layer , so dedivering a highly-availabe service on top of a cluster of computers.

	The project includes these modules:

	Haddop COmmon: The common utilities that support the other Hadoop modules.

	Hadoop Distribuated File System(HDFS): Adistributed file system hat provides high-throughput access to application data.

	Hadoop YARN:  A framework for job scheduling and cluster resource management.

	Hadoop MapReduce: A YARN-based system for parallel  processing of large data sets.

	Other Hadoop-related projects at Apache include:

	Ambari: A web-based tool for provisioning, managing, and monitoring Apache Hadoop clusters which includes support for Hadoop HDFS, Hadoop MapReduce, Hive, HCatalog, HBase,

	ZooKeeper, Oozie, Pig and Sqoop. Ambari also provides a dashboard for viewing cluster health such as heatmaps and ability to view MapReduce,

	Pig and Hive applications visually alongwith features to diagnose their performance characteristics in a user-friendly manner.

	Current version:  2.6.2

	* sequenceiq/hadoop-docker

	hadoop-cluster-docker



# How to build multi-node Hadoop Cluster based on Docker

	[How to build multi-node Hadoop Cluster based on Docker](http://cloud.51cto.com/art/201505/477851_all.htm)

	In this projects, I developed 4 docker iamges: serf-dnsmasq, hadoop-base, hadoop-master, hadoop-slave

	* serl-dnsmasq

	Base on ubuntu:15.04, serf and dnsmasq are installed for providing DNS service for the Hadoop Cluster

	* Hadoop-base

	Base on serf-dnsmasq, openjdk, openssh-server, vim and Hadoop 2.3.0 are installed

	* hadoop-master

	Base on hadoop-base . Configure the Hadoop master node

	* hadoop-slave

	Based on hadoop-base. Configure the Hadoop slave node.

## Steps to build a 3 nodes Hadoop cluster

	1. pull images

			sudo docker pull kiwenlau/hadoop-master:0.1.0

            sudo docker pull kiwenlau/hadoop-slave:0.1.0

            sudo docker pull kiwenlau/hadoop-base:0.1.0

            sudo docker pull kiwenlau/serf-dnsmasq:0.1.0

	2. clone source code

		git clone https://github.com/kiwenlau/hadoop-cluster-docker

	3. run container

		 cd hadoop-cluster-docker

        ./start-container.sh

    4. test serf and dnsmasq service

        In fact, you can skip this step and just wait for about 1 minute.  Serf and dnsmasq need some time to start service. you can wait for a while if any nodes don't show up sice serf agent need time

        to recognize all nodes

        list all nodes of hadoop cluster

            serf members

		ssh slave2.kiwenlau.com

	5. start hadoop

			./start-hadoop.sh

	6. run wordcount

			./run-wordcount.sh

## Steps to build arbitrary size Hadoop cluster

	1. preparation

		check the steps 1~2 of section 1: pull images and clone source code

	2. rebuild hadoop-master

		./resize-cluster.sh 5

	3. start container

		./start-container.sh 5

		you'd better use the same parameter as the step b

	4. run the hadoop cluster

		check the steps 4~6 of section1: test serf and dnsmasq, start Hadoop and run wordcount

		plase test serf and dnsmasq service before start hadoop

