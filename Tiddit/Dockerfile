FROM ubuntu:20.04
MAINTAINER Georgie Samaha <georgiesamaha@gmail.com>

# Update the package repository and install dependencies
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        git \
        build-essential \
        cmake \
        libbz2-dev \
        liblzma-dev \
        libncurses5-dev \
        zlib1g-dev \
        libcurl4-gnutls-dev \
        libssl-dev \
        wget \
        python3 \
        python3-pip

# Install python dependencies
RUN pip3 install numpy cython joblib

# Clone and install TIDDIT
WORKDIR /usr/local
RUN git clone --branch TIDDIT-3.5.2 https://github.com/SciLifeLab/TIDDIT.git
RUN cd TIDDIT && \
    pip3 install -e .

# Clone and build fermi2, ropebwt2 and bwa
RUN git clone https://github.com/lh3/fermi2.git && \
    cd fermi2 && \
    make && \
    ln -s /usr/local/fermi2/fermi2 /usr/local/bin
RUN git clone https://github.com/lh3/ropebwt2.git && \
    cd ropebwt2 && \
    make && \
    ln -s /usr/local/ropebwt2/ropebwt2 /usr/local/bin
RUN git clone https://github.com/lh3/bwa.git && \
    cd bwa && \
    make && \
    ln -s /usr/local/bwa/bwa /usr/local/bin

# Set the working directory to /data
WORKDIR /data