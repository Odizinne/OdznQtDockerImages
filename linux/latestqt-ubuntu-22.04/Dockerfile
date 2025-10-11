FROM ubuntu:22.04
ARG QT_VERSION=6.10.0
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
    patchelf \
    unzip \
    zip \
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
    libdbus-1-3 \
    locales \
    rsync \
    curl \
    openssh-client \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*
# Install Node.js 22 from NodeSource
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
RUN ln -s /usr/bin/python3 /usr/bin/python
RUN pip install aqtinstall
RUN aqt install-qt linux desktop ${QT_VERSION} linux_gcc_64 -O /opt/Qt -m qt5compat qthttpserver qtimageformats qtmultimedia qtshadertools qtwebsockets
ENV PATH="/opt/Qt/${QT_VERSION}/gcc_64/bin:${PATH}"
ENV QT_PLUGIN_PATH="/opt/Qt/${QT_VERSION}/gcc_64/plugins"
ENV QML_IMPORT_PATH="/opt/Qt/${QT_VERSION}/gcc_64/qml"
WORKDIR /workspace
