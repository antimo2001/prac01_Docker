# For practicing Docker

- I am using the Getting Started tutorial found online [here](https://docs.docker.com/get-started/part2/)

## Hierarchy of an app is the following

- Stack
- Service
- Container (bottom most of this hierarchy)

## Run the app

syntax of the run command is

```bash
docker run -p ${HOSTPORT}:${PUBLISHPORT} friendlyhello
```

To find the IP address, use the command docker-machine ip: `docker-machine ip`

## hub.docker.com Credentials: my user/pwd is antimo/01q===

## List of docker commands from the Getting Started tutorial part 2

```bash
docker build -t friendlyhello .  # Create image using this directory's Dockerfile
docker run -p 4000:80 friendlyhello  # Run "friendlyhello" mapping port 4000 to 80
docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
docker container ls                                # List all running containers
docker container ls -a             # List all containers, even those not running
docker container stop <hash>           # Gracefully stop the specified container
docker container kill <hash>         # Force shutdown of the specified container
docker container rm <hash>        # Remove specified container from this machine
docker container rm $(docker container ls -a -q)         # Remove all containers
docker image ls -a                             # List all images on this machine
docker image rm <image id>            # Remove specified image from this machine
docker image rm $(docker image ls -a -q)   # Remove all images from this machine
docker login             # Log in this CLI session using your Docker credentials
docker tag YourImage YourUsername/YourRepository:YourTag  # Tag <image> for upload to registry
docker push YourUsername/YourRepository:YourTag            # Upload tagged image to registry
docker run YourUsername/YourRepository:YourTag                   # Run image from a registry
```

## Services are really just “containers in production.”

A service only runs one image, but it codifies the way that image runs—what ports it should use, how many replicas of the container should run so the service has the capacity it needs, and so on. Scaling a service changes the number of container instances running that piece of software, assigning more computing resources to the service in the process.

## Services: (docker-compose.yml)

A registry is a collection of repositories, and a repository is a collection of images—sort of like a GitHub repository, except the code is already built. An account on a registry can create many repositories.

## Appendix: Docker Terminology

- Image: an installation of software (it is NOT running yet)
- Container: a running app of your software (like a Virtual Machine that has been booted up)
- Repository: contains a group of Docker Images
- Registry: contains a group of Docker Repositories
- Service: is a dockr container and is usually grouped with other services to collaborate together
