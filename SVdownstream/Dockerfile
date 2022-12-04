FROM rocker/rstudio:4.0.3
MAINTAINER Georgie Samaha <georgiesamaha@gmail.com>

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

RUN R -e "install.packages('BiocManager', dependencies=TRUE)"
RUN R -e "BiocManager::install('StructuralVariantAnnotation')"