---
layout: post
title: Adding 404 Page in Tomcat
author: digvijayb
tags:
  - java
  - tomcat
  - web
date: 2022-05-15T09:59:42.780Z
description: How to move docker-desktop-data from one drive to another drive?
thumbnail: /images/uploads/error-page-404.png
---
# **How to add custom error pages in Tomcat 9?**

![404 Error Page](/images/uploads/error-page-404.png "tomcat custom 404 page")

We are going added two custom error pages one is 404 and one all the other errors for tomcat 9. we’ll start with creating error pages and added it to webapps directory of tomcat.

<!--more-->

I have added two pages **404.html** and **error.html** under *webapps/error*

Now we need to edit `server.xml` and added following code under **Host** tag

```xml
<Valve className="org.apache.catalina.valves.ErrorReportValve" 
       showReport="false" showServerInfo="false" 
       errorCode.404="webapps/error/404.html" 
       errorCode.0="webapps/error/error.html" />
```