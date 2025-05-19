FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y \
    x11-apps \
    gedit \
    #python3 python3-pip \
    libgtk-3-dev \
    && apt clean

RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    xz-utils \
    ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Toolchain for Linux desktop dev
RUN apt-get update && apt-get install -y \
    clang-14 \
    cmake \
    ninja-build \
    && ln -s /usr/bin/clang++-14 /usr/bin/clang++ \
    && ln -s /usr/bin/clang-14 /usr/bin/clang \
    && apt-get clean


# Set Flutter version
ENV FLUTTER_VERSION=3.22.0
ENV FLUTTER_HOME=/opt/flutter

# Download and install Flutter from the official archive
RUN curl -L https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}-stable.tar.xz \
    | tar -xJ -C /opt \
    && mv /opt/flutter /opt/flutter-${FLUTTER_VERSION} \
    && ln -s /opt/flutter-${FLUTTER_VERSION} $FLUTTER_HOME \
    && $FLUTTER_HOME/bin/flutter doctor

# Mark Flutter directory as safe for Git
RUN git config --global --add safe.directory /opt/flutter-3.22.0

# Set environment variables for Dart and Flutter paths
ENV PATH="/opt/flutter/bin:/opt/flutter/bin/cache/dart-sdk/bin:${PATH}"

CMD ["bash"]
