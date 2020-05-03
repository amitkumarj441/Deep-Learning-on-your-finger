FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu16.04

LABEL maintainer Amit Kumar Jaiswal <amitkumarj441@gmail.com>

#### CUDA dependencies
RUN echo "/usr/local/cuda-10.1/lib64/" >/etc/ld.so.conf.d/cuda.conf
RUN echo "/usr/local/cuda/extras/CUPTI/lib64/" >>/etc/ld.so.conf.d/cuda.conf

# check how to bind host provided libraries
# see https://github.com/singularityware/singularity/issues/611
RUN mkdir -p /host-libs && \
    echo "/host-libs/" >/etc/ld.so.conf.d/000-host-libs.conf
    
RUN apt-get update && apt-get install curl wget -y

RUN cd /opt && \
    wget -nv https://root.cern.ch/download/root_v6.10.02.Linux-ubuntu16-x86_64-gcc5.4.tar.gz && \
    tar xzf root_v6.10.02.Linux-ubuntu16-x86_64-gcc5.4.tar.gz && \
    rm -f root_v6.10.02.Linux-ubuntu16-x86_64-gcc5.4.tar.gz && \
    cd /opt/root/ && \
    /bin/bash bin/thisroot.sh

# Bazel dependencies for TF
RUN echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" >/etc/apt/sources.list.d/bazel.list && \
    curl https://bazel.build/bazel-release.pub.gpg | apt-key add -

# OpenAI visualisation libraries
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && apt-get install -y --allow-unauthenticated \
    build-essential \
    curl \
    git \
    libfreetype6-dev \
    libpng12-dev \
    libxpm-dev \
    libzmq3-dev \
    module-init-tools \
    pkg-config \
    python \
    python-dev \
    python3.5 \
    rsync \
    software-properties-common \
    unzip \
    zip \
    zlib1g-dev \
    openjdk-8-jdk \
    openjdk-8-jre-headless \
    vim \
    wget \
    bazel \
    python3-pip \
    python3-pip \
    xvfb \
    python-opengl \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip && \
    pip3 install --upgrade pip
