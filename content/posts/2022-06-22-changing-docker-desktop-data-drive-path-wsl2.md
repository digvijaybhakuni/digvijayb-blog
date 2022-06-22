---
layout: post
title: Changing docker-desktop-data drive path WSL2
author: digvijayb
tags:
  - docker
  - windows
date: 2022-06-21T13:24:26.568Z
thumbnail: /images/uploads/featured.png
---
Docker desktop uses windows WSL2 (window subsystem for linux) to create VM (virtual machine), after docker desktop installation two WSL2 VM gets created. **docker-desktop** and **docker-desktop-data**.

![docker logo](/images/uploads/featured.png "Docker Destop")

<!--StartFragment-->

docker-desktop-data VM have all the user data so, we will create copy of docker-desktop-data then remove existing one and mount the copy data to different drive path.

<!--EndFragment-->

<!--StartFragment-->

```
//Exporting Data to tar
wsl --export docker-desktop-data d:/wsl2/docker-data/data.tar//Deleting existing docker data 
wsl --unregister docker-desktop-data//Importing tar to new location
wsl --import docker-desktop-data d:\wsl\docker-data d:\wsl\docker-data\data.tar
```

<!--EndFragment-->