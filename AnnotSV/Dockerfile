FROM ubuntu:18.04
MAINTAINER Georgie Samaha <georgiesamaha@gmail.com>

RUN apt-get update -y && apt-get install -y \
  curl \
  g++ \
  libbz2-dev \
  liblzma-dev \
  make \
  python \
  tar \
  tcl \
  tcllib \
  unzip \
  wget \
  zlib1g-dev

ENV BEDTOOLS_INSTALL_DIR=/opt/bedtools2
ENV BEDTOOLS_VERSION=2.28.0
ENV ANNOTSV_VERSION=v3.1.3
ENV ANNOTSV=/opt/AnnotSV_$ANNOTSV_VERSION

WORKDIR /tmp
RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.28.0/bedtools-2.28.0.tar.gz && \
  tar -zxf bedtools-2.28.0.tar.gz && \
  rm -f bedtools-2.28.0.tar.gz

WORKDIR /tmp/bedtools2
RUN make && \
  mkdir --parents $BEDTOOLS_INSTALL_DIR && \
  mv ./* $BEDTOOLS_INSTALL_DIR

RUN ln -s $BEDTOOLS_INSTALL_DIR/bin/* /usr/bin/ && \
  rm -rf /tmp/bedtools2

RUN wget https://github.com/lgmgeo/AnnotSV/archive/refs/tags/v3.1.3.zip && \
  unzip v3.1.3.zip && \
  mv AnnotSV-3.1.3 ${ANNOTSV} && \
  rm v3.1.3.zip && \
  cd ${ANNOTSV} && \
  make PREFIX=. install

ENV PATH="${ANNOTSV}/bin:${PATH}"