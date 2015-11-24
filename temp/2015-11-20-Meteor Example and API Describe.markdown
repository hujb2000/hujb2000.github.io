---
layout: post
title:  "Meteor Example and API Describe"
date:   2015-11-20 13:35:30
categories: allen.hu update
---


12.  Meteor Documents Reading Notes

	1. Reactive

	2. One Language: JavaScript

	3. Three steps crate demo app

	Principles of Meteor

	1. Data on wire

	2. One Language, One data format: JSON

	3. Database Everywhere,

	4. Ltency Compensation

	5. Full Stack Reactivity

	6. Embrace the Ecosystem

	7. Simplicity Equals  Productivity

	* Structuring your application

	 1. Special Directories

	 * client

	 * server

	In Meteor, Your server code runs in a single thread per request, not in the asynchronous callback style typical of Node. We find the linear execution model a better fit fo the typical server code  in a

	Meteor application.

	 * public

	 * private

	 * client/compatibility

	 * tests/

	 * node_modules

	 2.  Files outside special directories

	 3. Example File Structure

	 4. File Load Order

	 5. Organizing Your Project

	 6. Data and Security

	 7. Authentication and user accounts

	 8. Input validation

	 9. Reactivity

	 [Reactive programming](https://en.wikipedia.org/wiki/Reactive_programming)

	10. Live HTML templates

		Spacebars is the onlyy templating system.

	11. Using packages

	meteor search,  meteor show,  meteor remove,  meteor update, meteor list

	12. Namespacing

	13. Deploying

		* Running on Meteor's infrastructure

		meteor deploy myapp.meteor.com

		Your application is now available at myapp.meteor.com

		* Running on your own infrastructure

		meteor build my_directory

		This command will generate a fully-contained Node.js application in the form of a tarball, To run this application , you need to provide Node.js 0.10 and a MongoDB server

		cd my_directory

		cd programs/server && npm install

		env PORT=3000 MONGO_URL=mongodb://localhost:27017/myapp node main.js


	14. Writing packages

		meteor create --package username:packagename ,  package.js

		meteor add [packagename]

		.versions file, This file specifies the versions of al packages used to build your package and is part of the source. Check it into version control to ensure

		repeatable builds across machines.



# Meteor API

##  Core

## Publish and subscribe

## Methods

## Check

## Server connections

	These functions manage and inspect the network connection between the Meteor client and server.

## Collections

## Session

	Session provides a global object on the client that you can use to store an arbitrary set of key-value paires. use it to store things like the currently selected item in a list.

	What's specail about Session is that it's reactive ,If you call Session.get("currentList") from inside a template , the template will automatically be rerendered wherenver Session.set("currentList",x) is called;

## Accounts

	The Meteor Accounts system builds on top of the userId support in publish and methods.  The core pacakges add the concept of user documents stored in the database , and additional package add secure password authentication,

	integration with third party login services. and a pre-built user interface.

## Accounts(multi-server)

## Passwords

	The accounts-password package contains a full system for password-based authentication. In addition to the basic username and password-base sign-in process, It also supports email-based sign-in include address verification and password recovery emails.

## Templates

	When you write a template as <template name="foo"> ... </template> in an HTML file in your app, Meteor generates a "template object" named Template.foo.

	Note that template name cannot contain hyphens and other special characters.

## Blase

	Blaze is the package that makes reactive templates possible. You can use the Blaze API directly in order to render templates programmatically and manipulate "Views," the building blocks of reactive templates. For more information, check out the Blaze project page.





## Mobile Config File

I your Meteor application targets mobile platform such as iOS or Android, you can configure your app's metadata and  build  process in a special top-level file called mobile-config.js

[Cordova config.xml](http://cordova.apache.org/docs/en/5.1.1/config_ref/index.html#The%20config.xml%20File_core_configuration_elements)



# Packages

Total :8667

* upload-jquery

* search

# shareit

# roles

# stars rating

# mysql

# angular-chart-js

# mocha-package

# accounts-steam

	Steam OpenID integration for Meteor Accounts

# ui menu

* neo4j

* utilities-react

* img-qrcode

	Provides template to generate QR code in <img> tag.

* highcharts

	HighCharts for Meteor, with an easy to use helper to get your started.

* phantomjs

* webpack:hot-reload

	Plug webpack hot reload middleware to Meteor

* table/grid

	All tables supoort sorting by one column, hence the first column is "mutli-column sorting" . Clicke the "Columne" button to display more features in the comparison table


## Most used

* meteor-base

A default set of  packages that almost every app will have, You should noly remove this package if your really, really know what you are doing.

It comes with the following packages.

1. meteor

2. webapp

3. underscore

4. hot-code-push

5. ddp

* mongo

Adaptor for using MongoDB and Minimongo over DDP

Direct access to npm mongodb API

* jquery

Manipulate the DOM using CSS selectors

This package is automatically include in every new Meteor app  by meteor create .

* standard-minifiers

Standard minifiers used with Meteor apps by default

* Session

The session is only used in the client , not for the server.


* Tracker

Dependency trakcer to allow reactive callbackes

Meteor Tracker is an incredibly tiny(~1k) but incredibly power ful library for transparent reactive programming in JavaScript, Tracker gives you much of the power of a full-blown

[Functional Reactive Program(FRP](https://en.wikipedia.org/wiki/Functional_reactive_programming) system without requireing you to rewrite your program as a FRP data flow graph, Combined with

Tracker-aware libraries. this lets you build complex event-driver programs without writing a lot of biolerplate event-handling code.

Tracker-aware libraries from the Meteor Project

1. Blaze

2.  Minimongo

3. Reactive-dict

* mobile-experience

A set of Cordova/PhoneGap-specific packages that set some good defaults when building for mobile, These packages only activate when you are building a native Android or iOS app.

	1. fastclick avoid the 300ms touch delay

	2. mobile-status-bar avoid the status bar information covering up your app content

	3. launch-screen  cover the app with a launch image so that people don't have to see things loading

* blaze-html-templates

Compile HTML templates into reactive UI with Meteor Blaze

A  meta-package that includes everything your need to compile and run Meteor templates with Spacebars and Blaze

1. templating: compiles .html files

2. blaze : the runtime library

3. spacebars: the templating language

* check

# momentjs

* scss

* logging

Logging facility

* reload

* fontawesome

* fast-render html-reporter

* i18n

* kadira-profiler

* flow-router

* iron-router-progress

* synced-cron

	Allows you to define and run scheduled jobs across multiple servers.

* force-ssl

* aggregate

	Proper MongoDB aggregations support for Meteor

* spin

	Simple spinner package for Meteor

* react

	Everything your need to use React with Meteor

* webapp

* migrations

Define and run db migrations

* browser-detection

Meteorite package that provides browser detection

* meteor-down

	Load Testing Framework for Meteor

* gridfs

	GridFS storage adapter for CollectionsFS

* camera

* materialize

Materialize(official)): A modern responsive front-end framework based  on Material Design

* graphicsmagick

* iron-router-ga

Google analytics(universal edition) with some Iron Router sugar for tracking page views.

* lodash

* admin

* highcharts

* browser-policy

Configure security policies enforced by the browser.

* babel

* ionicons-sass

* ionic-sass

* honeypot

Plugin to define a honeypot captcha template to protect your forms from spambots

* autoform-file

* blaze-meta

Blaze-meta makes it super simple to manager SEO data

* sweetalert

* push

Isomorphic Push notifications  for APN and GCM

* autoform-modals

Create , update, and delte collections with modals

* autoform-map

Edit location coordinates with autoForm

* slingshot

Directly post f iles to clound storage services, such as AWS-s3

* momentum

Reactive animations


#  Meteor

## Slow Start

    git clone git://github.com/meteor/meteor.git

    cd meteor

    ./scripts/generate-dev-bundle.sh


	root

	./meteor --help

	cd docs

	../meteor

## Uninstalling Meteor

	rm -rf ~/.meteor/

    sudo rm /usr/local/bin/meteor
