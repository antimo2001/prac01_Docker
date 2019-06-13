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

## Swarms

A swarm is a group of machines that are running Docker and joined into a cluster. After that has happened, you continue to run the Docker commands you’re used to, but now they are executed on a cluster by a swarm manager. The machines in a swarm can be physical or virtual. After joining a swarm, they are referred to as nodes.

Swarm managers can use several strategies to run containers, such as “emptiest node” -- which fills the least utilized machines with containers. Or “global”, which ensures that each machine gets exactly one instance of the specified container. You instruct the swarm manager to use these strategies in the Compose file, just like the one you have already been using.

Swarm managers are the only machines in a swarm that can execute your commands, or authorize other machines to join the swarm as workers. Workers are just there to provide capacity and do not have the authority to tell any other machine what it can and cannot do.

Up until now, you have been using Docker in a single-host mode on your local machine. But Docker also can be switched into swarm mode, and that’s what enables the use of swarms. Enabling swarm mode instantly makes the current machine a swarm manager. From then on, Docker runs the commands you execute on the swarm you’re managing, rather than just on the current machine.

## Appendix: Docker Terminology

- Image: an installation of software (it is NOT running yet)
- Container: a running app of your software (like a Virtual Machine that has been booted up)
- Repository: contains a group of Docker Images
- Registry: contains a group of Docker Repositories
- Service: is a docker container and is grouped with other services to collaborate together
- Task: a single container running within a service
- Swarm: is a group of services? that's either running/not-running?
- Swarm Mode: enables Docker to be used within a multi-host node cluster (a cluster of Docker machines)
- Swarm Manager: is what it sounds like ...a cluster can only have 1 manager?
- Swarm Master: is synonymous with a Swarm Manager?
