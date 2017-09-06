---
author: zeddified
comments: true
excerpt: 'Setting the Go Build env'

slug: setting-go-build-env
title: Setting the Go Build env
categories:
- Technotes
tags:
- Technotes
- Zed

image_path: "/img/colours/goldfish.png"

---

In relation to: [Scalable Microservices with Kubernetes — Building Containers with Docker: Creating the Image](https://classroom.udacity.com/courses/ud615/lessons/7826816435/concepts/81980819570923#)

When building Go binaries for a Linux container in a non-Linux environment, you have to specify a Linux environment when running the build command.

1. Run ```env```. BSD command that (1) modifies the runtime environment and then (2) runs a specified utility. Syntax is usually ```env <ENVIRONMENT VARIABLES> <UTILITY TO RUN -PARAMETERS>```

2. Specify environment in key=value pairs to match the container environment. In the case of Alpine Linux Docker images, specify the environment as ```GOOS=linux GOARCH=386```.

3. Run the "go build" utility. In this context, the environment is set such that the utility will build for a Linux i386 environment.

4. Attach flags to build with static binaries.
4.1. ```--tags netgo``` forces Go to build binaries with the Go network's library instead of the host's libraries.
4.2. ```--ldflags "-extldflags '-lm -lstdc++ -static'" passes "-extldflags '…'"``` as arguments for every Go tool link invocation. Arguments are read as a space separated string.
4.3. ```-extldflags '-lm -lstdc++ -static'``` builds the Go binary with static libraries. Libraries included are: lm, lstdc++, static(?).

Complete command:
```
env GOOS=linux GOARCH=386 go build --tags netgo --ldflags "-extldflags '-lm -lstdc++ -static'"
```