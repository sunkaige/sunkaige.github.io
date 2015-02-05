# 优秀的Web开发框架、库和工具指南

本文列举了一组优秀的用于Web开发的框架、库和工具，可以作为项目架构阶段的参考。所有的资源都是开源的。

内容也会不断补充。

## 统一的虚拟开发环境
### Vagrant
Vagrant是一个基于命令行的虚拟机管理工具。它能帮助你快速搭建虚拟机开发环境。

建议为每个项目单独建立一套虚拟环境，开发者可以很方便的在多个虚拟环境中切换。

操作系统推荐使用Ubuntu 12.04 LTS 64bit, 已有标准镜像提供下载。具体请参考[这篇文章](vagrant-guide.md)。

### Docker
Docker是一种崭新的虚拟化容器技术，可以考虑在项目中试验性的使用。

## 网页应用
### 单页面的网站

**前端**

JavaScript框架

  1. Angular JS
  2. Backbone
  3. Jquery or zeptojs

CSS preprocessors

  1. LESS
  2. SASS and Compass

Theme

  1. Bootstrap 3
  2. Foundation
  3. Ionic Framework (Require AngularJS | Mobile)

Tools & Workflow

  1. NodeJS
  1. Yeoman
  1. Grunt(or Gulp)
  1. Bower

包依赖管理

  1. RequireJS

Icon Font

  1. Font Awesome

**后端**

在单网页应用中，后端只需要提供RESTful的服务。

根据不同开发语言，有以下框架可供选择：

Java

  1. Drop Wizard
  2. Spring Boot
  3. Spark

NodeJS

  1. restify
  1. Connect

PHP

  1. Slim

Ruby

  1. Sinatra

Python

  1. Flask

### 多网页的网站

需要使用MVC框架来搭建。根据语言不同，有以下框架可供选择：

Java

  1. Spring MVC Framework
  2. Nanja Framework

Scala

  1. Play Framework

NodeJS

  1. Express

PHP

  1. Yii framework
  1. Laravel
  1. Wave Framework

Ruby

  1. Rail

Python

  1. Django

### Package Repository Mirror
RubyGems (http://ruby.taobao.org)

NodeNPM (http://npm.taobao.org)

### Frontend CDN
http://libs.useso.com/

## 构建工具
Java

  1. Gradle
  2. Maven

Frontend

  1. Grunt

## Web Server

### Java Container
1. tomcat
1. jetty

### Http Server
1. Nginx
2. apache

## Reverse Proxy
1. Nginx

## Load Balancer
1. Nginx
1. HAProxy

## Page Cache
1. Nginx
2. Vanish

## Distributed App Cache
1. Redis
1. memcached

## Relational Database
1. Mysql
2. Postgres
3. MariaDB

## NoSQL Database
1. Mongo

## Message Queue
1. RabbitMQ

## Continous Integration
1. Jenkins

# 可供参考学习的开源网站
1. Taiga.io. (https://github.com/taigaio)  
   Your Agile, Free and Open Source Project Management Tool  
   `AngularJS + Django`

2. Humhub (https://github.com/humhub/humhub)  
   Open source Social Network  
   `Yii framework`

3. Guardian Frontend (https://github.com/guardian/frontend)  
   `Play framework`