# MyDockerfiles
Bioinformatics dockerfiles for:
* [SomaticStructuralV-nf GPL reporting]()
* [GermlineStructuralV-nf downstream analysis in RStudio]()
* [AnnotSV structural variant annotation]() 

# Build method

**1. Create a new directory for your Dockerfile**

For example:
```
mkdir SVdownstream
```

**2. Create a new file in the directory named `Dockerfile`**

For example:
```
nano Dockerfile
```

**3. Choose a base image to start from**

Add this to the first line of the Dockerfile. For example:
```
FROM rocker/rstudio:4.0.3
```

**4. Add any dependencies that your application needs**

Add these to your Dockerfile. For example:

```
RUN apt-get update -qq && apt-get -y --no-install-recommends install \
libxml2-dev \
libcairo2-dev \
libsqlite-dev \
libmariadbd-dev \
libmariadbclient-dev \
libpq-dev \
libssh2-1-dev \
unixodbc-dev \
libsasl2-dev \
&& install2.r --error \
--deps TRUE \
tidyverse \
knitr \
devtools \
formatR \
remotes \
selectr \
caTools
```

**5. Configure any environment variables or other settings**

For example:
```
```

**6. Define any commands or entrypoints to run when the container starts**

**8. Build the image**

For example:
```
sudo docker build -t svdownstream:1.0 .
```

**9. Build .sif with singularity**

For example:
```
sudo singularity pull docker-daemon:svdownstream:1.0
```