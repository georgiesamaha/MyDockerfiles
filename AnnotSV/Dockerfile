FROM ubuntu:18.04
MAINTAINER Georgie Samaha <georgina.samaha@sydney.edu.au>

LABEL \
  version="1.0" \
  description="AnnotSV v3.1.3 container developed for GermlineStructuralV-nf pipeline"

RUN apt-get update -y && apt-get install -y \
  bzip2 \
  curl \
  g++ \
  libbz2-dev \
  liblzma-dev \
  libcurl4-gnutls-dev \
  make \
  python \
  tar \
  tcl \
  tcllib \
  unzip \
  wget \
  zlib1g-dev

# set environmental variables
ENV BEDTOOLS_INSTALL_DIR=/opt/bedtools2
ENV BCFTOOLS_INSTALL_DIR=/opt/bcftools
ENV BEDTOOLS_VERSION=2.28.0
ENV BCFTOOLS_VERSION=1.16
ENV ANNOTSV_VERSION=v3.1.3
ENV ANNOTSV=/opt/AnnotSV_$ANNOTSV_VERSION

# install bedtools2
WORKDIR /tmp
RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.28.0/bedtools-2.28.0.tar.gz && \
  tar -zxf bedtools-2.28.0.tar.gz && \
  rm -f bedtools-2.28.0.tar.gz

WORKDIR /tmp/bedtools2
RUN make && \
  mkdir --parents $BEDTOOLS_INSTALL_DIR && \
  mv ./* $BEDTOOLS_INSTALL_DIR

WORKDIR /
RUN ln -s $BEDTOOLS_INSTALL_DIR/bin/* /usr/bin/ && \
  rm -rf /tmp/bedtools2

# install bcftools
WORKDIR /tmp
RUN wget https://github.com/samtools/bcftools/releases/download/$BCFTOOLS_VERSION/bcftools-$BCFTOOLS_VERSION.tar.bz2 && \
  tar --bzip2 -xf bcftools-$BCFTOOLS_VERSION.tar.bz2

WORKDIR /tmp/bcftools-$BCFTOOLS_VERSION
RUN make prefix=$BCFTOOLS_INSTALL_DIR && \
  make prefix=$BCFTOOLS_INSTALL_DIR install

WORKDIR /
RUN ln -s $BCFTOOLS_INSTALL_DIR/bin/bcftools /usr/bin/bcftools && \
  rm -rf /tmp/bcftools-$BCFTOOLS_VERSION

# install annotsv
WORKDIR /opt
RUN wget https://github.com/lgmgeo/AnnotSV/archive/refs/tags/v3.1.3.zip && \
  unzip v3.1.3.zip && \
  mv AnnotSV-3.1.3 ${ANNOTSV} && \
  rm v3.1.3.zip && \
  cd ${ANNOTSV} && \
  make PREFIX=. install

ENV PATH="${ANNOTSV}/bin:${PATH}"

WORKDIR /
