FROM ubuntu:22.04
ARG QT_VERSION=6.9.3
ARG EMSDK_VERSION=3.1.70
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
    libgl1-mesa-dev \
    libxkbcommon-x11-0 \
    libxcb-icccm4 \
    libxcb-image0 \
    libxcb-keysyms1 \
    libxcb-randr0 \
    libxcb-render-util0 \
    libxcb-xinerama0 \
    libxcb-xfixes0 \
    libglib2.0-0 \
    locales \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

RUN ln -s /usr/bin/python3 /usr/bin/python

RUN pip install aqtinstall

# Install Emscripten
RUN git clone https://github.com/emscripten-core/emsdk.git /opt/emsdk && \
    cd /opt/emsdk && \
    ./emsdk install ${EMSDK_VERSION} && \
    ./emsdk activate ${EMSDK_VERSION}

# Set Emscripten environment variables
ENV EMSDK=/opt/emsdk
ENV PATH="${EMSDK}:${EMSDK}/upstream/emscripten:${PATH}"

# Install Qt to /opt/Qt
RUN aqt install-qt linux desktop ${QT_VERSION} linux_gcc_64 -O /opt/Qt -m qt5compat qthttpserver qtimageformats qtmultimedia qtshadertools qtwebsockets
RUN aqt install-qt all_os wasm ${QT_VERSION} wasm_singlethread -O /opt/Qt -m qt5compat qthttpserver qtimageformats qtmultimedia qtshadertools qtwebsockets

# Set Qt environment variables
ENV PATH="/opt/Qt/${QT_VERSION}/gcc_64/bin:${PATH}"
ENV QT_PLUGIN_PATH="/opt/Qt/${QT_VERSION}/gcc_64/plugins"
ENV QML_IMPORT_PATH="/opt/Qt/${QT_VERSION}/gcc_64/qml"
ENV QT_HOST_PATH="/opt/Qt/${QT_VERSION}/gcc_64"
ENV QT_WASM_PATH="/opt/Qt/${QT_VERSION}/wasm_singlethread"

WORKDIR /workspace