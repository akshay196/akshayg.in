---
title: Run ManageIQ using Docker
subtitle: Containerize ManageIQ
date: 2017-10-10
tags: [ManageIQ, Docker, setup]
---

Docker image for ManageIQ is available. It can be run in Docker
container. There are also other options like [Public
cloud](http://manageiq.org/docs/get-started/cloud) or
[Vagrant](http://manageiq.org/docs/get-started/vagrant) to get started
with ManageIQ. It can run everywhere Docker is available.

First thing, you have to install Docker in your system. Follow
instructions in [Docker
docs](https://store.docker.com/search?type=edition&offering=community)
to install Docker.

Start Docker service using

```bash
$ sudo service docker start
```

### Step 1: Pull Docker image of ManageIQ

```bash
$ sudo docker pull manageiq/manageiq:fine-3
```

It will download ManageIQ Fine-3 image from Docker registry. To see
image list, run this

```bash
$ sudo docker images ls
```

### Stpe 2: Run Docker container

```bash
$ sudo docker run --privileged -d -p 8443:443 manageiq/manageiq:fine-3
```

It will run container in detached mode. To see a list of running
containers, execute

```bash
$ sudo docker ps
```


Now ManageIQ container is up and running at IP address
[https://127.0.0.1:8443](https://127.0.0.1:8443)

It has username as *admin* and the password is *smartvm*. Get the
login and explore the world of ManageIQ.
