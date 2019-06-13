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

A single container running in a service is called a **task**. Tasks are given unique IDs that numerically increment, up to the number of replicas you defined in docker-compose.yml.

```bash
docker stack ls                                            # List stacks or apps
docker stack deploy -c <composefile> <appname>  # Run the specified Compose file
docker service ls                 # List running services associated with an app
docker service ps <service>                  # List tasks associated with an app
docker inspect <task or container>                   # Inspect task or container
docker container ls -q                                      # List container IDs
docker stack rm <appname>                             # Tear down an application
docker swarm leave --force      # Take down a single node swarm from the manager
```

## Appendix: Docker Terminology

- Image: an installation of software (it is NOT running yet)
- Container: a running app of your software (like a Virtual Machine that has been booted up)
- Repository: contains a group of Docker Images
- Registry: contains a group of Docker Repositories
- Service: is a docker container and is grouped with other services to collaborate together
- Task: a single container running within a service
- Swarm: is a group of services? that's either running/not-running?

