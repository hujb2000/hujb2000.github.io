---
layout: post
title:  "BIMServer"
date:   2016-07-26 13:35:30
categories: allen.hu update
---


# BIMServer

## BimServerWar

WarServerInitializer:


## BimServerJar

1. LocalDevBimServerStarter.java

new LocalDevBimServerStarter().start(-1, "localhost", 8080, 8085, new OptionsParser(args).getPluginDirectories());

BimServer

JarSettings

class Starter extends JFrame

## BimServerClientLib

This project provides a Java API for BIMserver. It can use a direct (in-JVM) connection to BIMserver, or SOAP, Protocol Buffers or JSON.

## PluginBase

This project contains code required for building plugins. This should be the only compile-time dependency you need. The only dependencies of this project are jar files that are available on maven repositories.


## Shared

This project contains code that is being shared between both the BIMserver project, and the BimServerClientLib.

##  BimServer

This is the main BIMserver project. The project provides:
- An EMF based database layer for BerkeleyDB Java Edition
- Database migrations
- API's (SOAP, Protocol Buffers, JSON)
- Mail templates
- Notification management
- Caching
- Plugin Management

## BIMsurfer

BIMsurfer如何作为插件进行发布

## bimvie.ws

Javascript client for Building Information Modelling, using open standards like IFC, BCF and BIMSie. Using Bootstrap, BIM Surfer, etc..

git submodule update

## CityGML

BIMserver plugin for CityGML output of models


At the moment the plugin does not work. Anyone interested in adopting this project, please let us know!

## BinarySerializers

BIMserver plugins that provide binary serializations of model data

## IfcOpenShell BIMServer plugin

IfcOpenShell BIMserver plugin

## Tools

This projects contains a few tools, mainly for research purposes.

## IfcValidator

Checking IFC models on the quality of the data. Implemented parts of the Dutch "Rijksgebouwendienst BIM norm" as an example.

Done: Ifc2x3tc1
ToDo: IFC4 as well

## WebGL-threeJS

WebGL viewer for BIMserver.org; based on ThreeJS

## BIMserver-Repository

Public repository for BIMserver services, plugins, extended data schema's and more

.gitmodules


##  DemoPlugins

BIMserver plugins for demo purposes

## IfcPlugins

BIMserver plugins that provide IFC serialization/deserialization

## COBie-plugins

 Pulse  Graphs
COBie import/export plugins for the open source BIMserver.org platform

## Mergers

BIMserver plugin that provide basic merging

## JavaModelChecker

BIMserver plugin that can do model checking based on (runtime configurable) Java code

## Charting

BIMserver plugin that can create all sorts of charts of your model

## bimql

Building Information Model Query Language (BimQL) http://www.bimql.org/

## IfcEngine

BIMserver plugin which provider a Render Engine by embedding the RDF Ifc Engine

## ClashDetectioService


A BIMserver plugin that does basic clash detection

For now this is just a place where we put the ClashDetectionService code, it is not actually working, but we will work on that soon.

This code has been migrated from the BIMserver main repository

## Console

Webbased tool for interactive BIMserver API access

## TestFiles

This project contains test (IFC) files

## BCF-Forum

Server and forum to communicate on BIM issues. BCF 2.0 compatible.

## floorplan-generator

Plug-in for BIMserver to create a 2D HTML floorplan generator.

This project depends on some of the resources included in the standard COBie plugins page (the COBieShared project).
Future revisions will eliminate the COBieShared dependency, but for now, you must import the COBieShared project (of the COBiePlugins repository)if you want to work with the source code.

j3dcore.jar, j3dutils.jar, and vecmath.jar must be in the Bimserver/lib directory. See Java3d/J3d.

The j3d dependencies need to be setup to point to the native dll (on windows machines). j3dcore-ogl.dll. We have been putting that dll in BimServer/native/j3dcore-ogl.dll

## bimvie.ws-viewer

New viewer for BIMVie.ws, in separate project for review before integration

## IFC-Files(2 years ago)

Goals of this repository is to create a library of IFC files for demonstration, testing, validation, etc.


## TestFramework


##Wiki

Memories:  number of objects( IFC model ), 12Gb Heap Size,  220Gb
BerkeleyDB cache: 25% of heap of BIMserver

64 bits system & 32GB of Memory: compressed oops


http://docs.oracle.com/javase/7/docs/technotes/guides/vm/performance-enhancements-7.html#compressedOop

JAR Starter

1.4 最后一版本，设置完后可以直接进入
1.5 不行



