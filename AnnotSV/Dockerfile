FROM ubuntu:20.04
MAINTAINER Georgie Samaha <georgiesamaha@gmail.com>
LABEL \
  version="3.1.2" \
  description="AnnotSV with dependencies"

## Install linux dependencies
RUN apt update && \
  DEBIAN_FRONTEND=noninteractive apt install -y wget \
  git \
  make \
  gcc \
  zlib1g-dev \
  liblzma-dev \
  libbz2-dev \
  libcurl4-gnutls-dev \
  tcl \
  pigz

## Install bedtools (dependency)
ENV BEDTOOLS_INSTALL_DIR=/opt/bedtools2
ENV BEDTOOLS_VERSION=2.30.0

RUN mkdir $BEDTOOLS_INSTALL_DIR
WORKDIR $BEDTOOLS_INSTALL_DIR
RUN wget https://github.com/arq5x/bedtools2/releases/download/v$BEDTOOLS_VERSION/bedtools.static.binary && \
	mv bedtools.static.binary bedtools && \
  	chmod a+x bedtools && \
	ln -s $BEDTOOLS_INSTALL_DIR/bedtools /usr/bin

## Install bcftools (dependency)
ENV SAMTOOLS_VERSION=1.14
WORKDIR /opt
RUN git clone --branch $SAMTOOLS_VERSION --recurse-submodules https://github.com/samtools/htslib.git && \
	git clone --branch $SAMTOOLS_VERSION https://github.com/samtools/bcftools.git
WORKDIR /opt/bcftools
RUN make && \
	ln -s /opt/bcftools/bcftools /usr/bin

## Install annotSV 
ENV ANNOTSV_INSTALL_DIR=/opt/AnnotSV
ENV ANNOTSV_VERSION=3.2.1

WORKDIR /opt
RUN git clone --branch v$ANNOTSV_VERSION https://github.com/lgmgeo/AnnotSV.git
WORKDIR $ANNOTSV_INSTALL_DIR
RUN make PREFIX=. install
ENV ANNOTSV=/opt/AnnotSV
ENV PATH=$PATH:$ANNOTSV_INSTALL_DIR/bin/

## Tidy up
RUN apt remove -y git wget
WORKDIR /
ADD Dockerfile /
