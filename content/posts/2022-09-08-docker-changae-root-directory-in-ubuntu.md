---
layout: post
title: "Docker: Changae Root Directory in Ubuntu "
Description: "\n\n\n\n\n\n"
author: digvijayb
tags:
  - docker
date: 2022-09-15T10:34:01.697Z
thumbnail: /images/uploads/featured.png
---
Install docker in your system as you like do using apt, snap or etc
<!--more-->
Now stop docker service 
```sh
$ sudo systemctl stop docket.socket
```
Create directory in your system, where your want to put your docker root
```sh
$ mkdir /mydata/docker-root
```
If you have some data in your old docker directory, you can copy that newer one, can use rsync for the same

```sh
sudo rsync -aqxP /var/lib/docker/ /mydata/docker-root
```