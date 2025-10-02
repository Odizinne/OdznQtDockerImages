FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y \
    build-essential \
    cmake \
    ninja-build \
    git \
    python3 \
    python3-pip \
    python3-dev \
    sudo \
    unzip \
    libglib2.0-0 \
    locales \
    rsync \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

# Create symlinks for python and pip (optional, but convenient)
RUN ln -s /usr/bin/python3 /usr/bin/python

WORKDIR /workspace