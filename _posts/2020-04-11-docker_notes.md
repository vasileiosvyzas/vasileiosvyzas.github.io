---
title: "Docker notes"
date: 2020-04-11
tags: [docker]
---

## What is it?
Docker is a tool that allows to built containers. Containers are isolated environments that wrap up a piece of software in a complete filesystem that contains everything it needs to run: code, runtime, system tools, system libraries - anything you can install on a server. This guarantees that it will always run the same, regardless of the environment it is running in.

Containers are useful because they allow a develop to package up their application and all its parts (the stack it runs on, libraries and dependencies) in that isolated environment and share the application with the developers, sys admins across different machines and environments. Basically, it gets rid of the old headache of 'it works on my machine'

## Containers are not VMs
![alt text](/image/docker/containers_photo.png)

- Containers virtualize the operating systems, VMs virtualize the hardware
- Multiple containers can run on the same machine and share the host OS kernel with other containers, multiple VMs can run on the same machine but each VM has a copy of an operating system.
- Containers take up less space than VMs and can handle more applications, VMs can be slow to boot.

## Docker benefits:
- Scalable: Containers are extremely lightweight which makes scaling up and scaling down very fast and very easy. We can launch more containers as we need them or shut them down when we no longer need them
- Density: Because we are dealing with isolated containers we can put more of them into our machines which means that we can make more efficient use of our resources which can result in fewer machines and also can lead to reducing licensing cost for the shared resources on a machine
- Portable: We can get a snapshot of our environment, upload it to a registry, download and start making applications out of it.
- Deployment: Containers can run almost anywhere, we can deploy to desktops, laptops, servers, virtual machines

## Docker Core Components
- Docker Daemon: Docker Engine, runs on the host machine
- Docker Client: CLI used to interact with the daemon
- Docker Image:
	The Docker Image is a template the containts the environment, base operating system & your application and the stack that it runs on and all its dependencies. These images are like an onion, they are layered 
- Docker container:
	Created from images. You spin up a container, specifying an image and there you have it. The actions you can do at a container are Start, stop, move, delete
- Docker registry:
	Public & private repositories used to store images. Public repositories are searchable via the docker hub. You don't need to start from scratch. You can search at DockerHub for an image where somebody has already built your environment, they already have a technology stack similar to what you want to use. You can use that as your base image and then customise it to your environment.
- Dockerfile:
	Automates image construction. Declarative way of setting up your images. We fill up this file with instructions and rather than doing it all manually like login on your base image and installing software, we can put all the commands on a file and use that file to automatically built an image.


## Best Practices
- Containers should be ephemeral.
    - If something has stopped working, kill it and start a new one. Don't store information in the container - mount volumes instead
- Use a .dockerignore file.
    - Don't copy over directories and files that are not important to the container
    - Containers should be as small as possible
- Avoid installing unnecessary packages
- Build from the cache
	- We can turn off the cache with the --no-cache flag
	- But why run yum update twice?
	- If files are added or copied a comparison is made to see if they have changed, if so it will spawn a new container
	- It will not check git repositories if you clone them directly
- FROM - Use official repositories
	- Your container will always run and be up to date
- Run - Format long commands to make them readable
	- Use the backsiashesto separate over lines
	- Don’t run upgrade as this will likely fail due to privileges
- ADD and COPY
	- They do similar things
	- If you don't need to get something from a URL or to decompress it then use COPY
	- Copy files individually so the cache will only invalidate a container when one file changes
	- You are discouraged from using ADD to get files from URLs. Use wget or curl
- ENTRYPOINT
	- Best practice is to use this for the command to be run when the container starts
	- use CMD as default flags

## Install docker
There may be an unrelated docker package already installed with Fedora
    - sudo yum —y remove docker
    
Install Docker-lO
    - sudo yum install docker—io

Start the service and ensure it starts at boot
    - sudo service docker start
    - sudo chkconfig docker on
