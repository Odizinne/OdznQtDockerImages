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
    && rm -rf /var/lib/apt/lists/*
# Create symlinks for python and pip (optional, but convenient)
RUN ln -s /usr/bin/python3 /usr/bin/python
WORKDIR /workspace
