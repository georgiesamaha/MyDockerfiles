# MyDockerfiles
 
# Build method

**1. Create a new directory for your Dockerfile**

For example:
```
mkdir SVdownstream && cd SVdownstream
```

**2. Create a new file in the directory named `Dockerfile`**

```
touch Dockerfile
```

**3. Choose a base image to start from**

Add this to the first line of the Dockerfile. Some examples:
```
FROM rocker/rstudio:4.0.3
FROM python:3.8-slim
FROM ubuntu:20.04
```

**4. Add any dependencies that your application needs**

To work out what is needed, look at install scripts or Dockerfile templates provided by the tool's developer. 

**5. Configure any environment variables or other settings**

To work out what is needed, look at install scripts or Dockerfile templates provided by the tool's developer. 

**6. Define any commands or entrypoints to run when the container starts**

To work out what is needed, look at install scripts or Dockerfile templates provided by the tool's developer. 

**8. Build the image**

For example:
```
sudo docker build -t <name>:<tagVersion> .
```

**9. Build .sif with singularity**

For example:
```
sudo singularity pull docker-daemon:svdownstream:1.0
```

**10. Upload to DockerHub**

On the Dockerhub website, select `Repositories` and then `Create repository`

From the command line: 
```
docker tag <local-image>:<tagVersion> <repo-name>:<tag-name>
docker push <new-repo>:<tag-name>
```