# Copyright (c) Facebook, Inc. and its affiliates. All Rights Reserved

FROM ubuntu:18.04

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
  build-essential \
  ca-certificates \
  cmake \
  curl \
  git \
  libcurl4-openssl-dev \
  libgflags-dev \
  unzip

# Install miniconda to /miniconda
WORKDIR /
RUN curl -LO http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -p /miniconda -b
RUN rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH=/miniconda/bin:${PATH}
RUN conda update -y conda

# Python packages from conda
RUN conda install -c anaconda -y python=3.7
RUN conda install thrift

# Install Thrift + dependencies
WORKDIR /
RUN apt-get update && apt-get install -y \
    libboost-dev \
    libboost-test-dev \
    libboost-program-options-dev \
    libboost-filesystem-dev \
    libboost-thread-dev \
    libevent-dev \
    automake \
    libtool \
    flex \
    bison \
    pkg-config \
    libssl-dev \
    && rm -rf /var/lib/apt/lists/*
RUN curl https://downloads.apache.org/thrift/0.13.0/thrift-0.13.0.tar.gz --output thrift-0.13.0.tar.gz \
    && tar -xvf thrift-0.13.0.tar.gz \
    && rm thrift-0.13.0.tar.gz
WORKDIR /thrift-0.13.0
RUN ./bootstrap.sh \
    && ./configure \
    && make \
    && make install

# to import 'client.py' in '/client/' folder
ADD client.py /client/
ADD challenge.thrft /client/


# to define '/client/' as base directory
WORKDIR /client/

# to create pen-py folder which includes the calculator serive
RUN thrift -r --gen py challenge.thrft