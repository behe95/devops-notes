# devops-notes - Docker

> Personal DevOps learning notes covering Linux, networking, SSH, backend deployment practices and others as needed.

Basic docker CLI commands for deploying a complete project.

---

### Note: `<value>` represents a variable to be replaced with actual value

## Images

---


```bash
docker iimages                                                        # List images.

docker pull <tag>                                                     # Download image

docker image rm <image-name|image-id>                                 # Remove image.

docker build -t <image-name:tag> </path/to>                           # Build docker image.
```


## Containers

---


```bash
docker ps                                                                             # List running containers.

docker ps -a                                                                          # List all containers (includes stopped containers)

docker run --name <container-name> <image-tag>                                        # Docker container create and run.

docker run -d --name <container-name> <image-tag>                                     # Create and run in detached mode.

docker run -d -p <host-PORT>:<container-PORT> --name <container-name> <image-tag>     # Port binding. <host-port> = port exposed on the host machine
                                                                                      # <container-port> = port the application listens on inside the container
  
docker run --env-file <env-file> --name <container-name> <image-tag>                  # Pass environment variables from a file


docker start <container-name|container-id>                                            # Start a stopped container

docker stop <container-name|container-id>                                             # Stop a running container

docker restart <container-name|container-id>                                          # Restart a container.


docker rm <container-name|container-id>                                               # Remove a container.

docker rm -f <container-name|container-id>                                            # Force remove a container.



docker exec -it <container-name|container-id> env                                     # Display environment variables inside the container.
```

