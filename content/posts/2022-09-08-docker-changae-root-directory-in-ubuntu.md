---
layout: post
title: "Docker: Changae Root Directory in Ubuntu "
Description: "**Change docker root directory for default path in ubuntu**"
author: digvijayb
tags:
  - docker
  - ubuntu
  - linux
  - ""
date: 2022-09-08T18:46:16.457Z
thumbnail: /images/uploads/featured.png
---
Install docker in your system as you like do using apt, snap or etc

<!--more-->

![Docker Logo](/images/uploads/featured.png)

Now stop docker service 

```sh
$ sudo systemctl stop docker.socket
```

Create directory in your system, where your want to put your docker root

```sh
$ mkdir /mydata/docker-root
```

If you have some data in your old docker directory, you can copy that newer one, can use rsync for the same

```sh
sudo rsync -aqxP /var/lib/docker/ /mydata/docker-root
```

Updating service file `/lib/systemd/system/docker.service`

```sh
$ sudo vi /lib/systemd/system/docker.service
```

will edit `ExecStart` property to add new data root `-g /mydata/docker-root`

```
ExecStart=/usr/bin/dockerd -g /mydata/docker-root -H fd://
```

Now, reload daemon and start docker again

```sh
$ sudo systemctl daemon-reload
$ sudo systemctl start docker
```

Once it is done we will verify it, and you should see new docker root

```sh
$ sudo docker info
```