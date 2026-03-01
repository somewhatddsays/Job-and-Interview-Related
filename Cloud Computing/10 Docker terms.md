# 10 Docker Terms that Save the day

## Docker Image
A read-only blueprint used to create container. Built from a Dockerfile and includes app code, dependencies, and environment setup.

>**Interview Tip:**
> 
> `Image: template`
> 
> `Container: running instance`


## Docker Container
A lightweight, isolated runtime created from an image. Runs your application with its own filesystem, network, and processes.

## Dockerfile
A script with instructions (FROM, RUN, COPY, CMD) used to build Docker images automatically.
> **Common Question:**
> 
> Difference between CMD vs. Entrypoint

## Layers
Each command in a Dockerfile creates a layer. Docker caches layers to make builds faster.
> **Optimization Trick:**
> 
> Put rarely changing steps first.

## Port Mapping
-p 3000:3000 maps container port &rarr; host port so your app is accessible outside Docker.

> Interviewers often ask why localhost doesn't work without it.

## Docker Network

Allows containers to communicate via service names, not IPs.

>**Key Concept:**
> 
> Containers on same network can talk like:
> 
> `https://backend:5000`
> 
> instead of using localhost

## Volumes

Persistent storage for containers. Prevent data loss when containers stop or restart.

>**Example:**\
> databases using Docker always need volumes.

## Docker Compose

Tool for defining multi-container apps using `docker-compose.yml`\
Used in real projects:
- frontend
- backend
- database
All started with one command.

# Registry
## (Docker Hub/ Private Registry)
A place where images are stored and pulled from.

**Flow**
>Build &rarr; Tag &rarr; Push &rarr; Pull &rarr; Run












