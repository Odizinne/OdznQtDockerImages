FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
    build-essential \
    cmake \
    git \
    python3 \
    python3-pip \
    python3-dev \
    sudo \
    libgl1-mesa-dev \
    libxkbcommon-x11-0 \
    libxcb-icccm4 \
    libxcb-image0 \
    libxcb-keysyms1 \
    libxcb-randr0 \
    libxcb-render-util0 \
    libxcb-xinerama0 \
    libxcb-xfixes0 \
    && rm -rf /var/lib/apt/lists/*

RUN ln -s /usr/bin/python3 /usr/bin/python

# Install aqt
RUN pip install aqtinstall

# Install Qt 6.9.3 with modules
RUN aqt install-qt linux desktop 6.9.3 linux_gcc_64 -m qt5compat qthttpserver qtimageformats qtmultimedia qtshadertools qtwebsockets

# Set Qt environment variables
ENV PATH="/opt/Qt/6.9.3/gcc_64/bin:${PATH}"
ENV QT_PLUGIN_PATH="/opt/Qt/6.9.3/gcc_64/plugins"
ENV QML_IMPORT_PATH="/opt/Qt/6.9.3/gcc_64/qml"

WORKDIR /workspace
