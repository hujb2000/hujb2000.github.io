---
layout: post
title:  "Paas-Flynn"
date:   2015-12-01 13:35:30
categories: allen.hu update
---

# Flynn


[Flynn](https://github.com/flynn/flynn) is designed to run anything that can run on Linux, not just stateless web apps. Flynn includes built-in database appliances(just Postgres right now) and handles TCP traffic as well as HTTP and HTTPS.

Eventually we want Flynn to be the only tool developers adn ops teams need to develop, deploy, and manage running software.



* Always open source

Flynn is 100% open source and will always be free. Usign Flynn donesn't lock you into any proprietary technology or  vendors. Flynn is developed in the open and al code is availabe on GitHub. Flynn is  open source , not "open core".
There are no special features available only to paying users. And there no limits on the number or type of servers , apps, or database you can use , You can deploy and scale as many apps and database on as many servers as you want

## Deploy

Flynn lets you deploy apps with ease. With built-in service discovery and GitHub integration , shipping your code has never been easier.

* API Driven

Flynn is entirely modular and API-driven, so you can easily modify or replace components and write your  own pipelines or workflows.

* Containers.

Flynn packages app as containers which maes them smaller, more portable, and efficient than VMs . Thousands of containers can run easily on a single machine.

* Deploy all your apps with Flynn.

Flynn turn s your code into containerized apps using buidpacks. It can connect to your GitHub accounts so you can deploy any of your repos with a single click , And if you've already packaged your apps as containers. Flynn can run those, too.

* Buildpacks

Flynn has built in support for most major languages and frameworks using buildpacks.

* Other apps.


* Batteries included.

After Flynn depolys your app. It can automatically provision and connect database and anything else your app needs.

* Flynn runs everywhere.

Flynn can run almost anywhere including public and private clouds, bare metal, or any combination. So you can swap infrastructure as you see fit.


## Scales up, scale out.

* Do more with less.

Flynn makes it easy to run many application on the same server. Which comes in handy, whether you want to run more services internally or make the most out of your hardware.

* Do more with more.

With Flynn you can run your apps on as many machines as your need, So when your apps are under heavy load they keep running.

* Do more together.

Flynn automatically find and connects all the components of your apps, Each container gets its own cluster-routable IP address . And because Flynn's service discovery system uses DNS you don't need to re-write our apps to use it .

* High availability

At scalse thing break. Flynn makes your applications resillient and fault-tolerant by running them across many machines. Flynn iteself is also highly available. So a single failure won't take down your cluster.

* The router

Flynn's built in router handles and load balances TCP and HTTPS traffic.

## Databases

Flynn databases are automatically backed up, helping your recover from mistakes. not just failures, Flynn builds database clusters in second, not hours, so developers can quickly stage and test changes.

* Data integrity

Flynn database use ZFS so even when the power goes out data is never corrupted.

Flynn databases automatically fail over. So there's no loss of data or downtime during a failure. And apps keep working without human intervention. Apps using Flynns service discovery are automatically configured and connected to built-in databases.


# Docs

* Cloud Install

L=/usr/local/bin/flynn && curl -sSL -A "`uname -sp`" https://dl.flynn.io/cli | zcat >$L && chmod +x $L

flynn install

* Manual Installation

