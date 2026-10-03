# This Dockerfile is intended for use with a Dev Container whose workspace folder
# is located on a Windows host. It intentionally assumes the root user to avoid
# permission compatibility issues between NTFS and Git.
# For the same reason, core.fileMode is set to false in the Git configuration.

FROM debian:13-slim

ENV LANG=C.UTF-8 \
    TZ=Asia/Tokyo

# Base
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        bubblewrap \
        ca-certificates \
        curl \
        fonts-morisawa-bizud-gothic \
        git \
        gnupg \
        jq \
        librsvg2-bin \
        libxml2-utils \
        lsb-release \
        openssh-client \
        unzip \
        vim \
        wget \
    && rm -rf /var/lib/apt/lists/* \
    && bash -c 'echo >> ~/.bashrc' \
    && bash -c 'echo "export PATH=\"\$PATH:~/.local/bin\"" >> ~/.bashrc' \
    && bash -c 'echo "export LS_OPTIONS=\"--color=auto\"" >> ~/.bashrc' \
    && bash -c 'echo "alias ls=\"ls \$LS_OPTIONS\"" >> ~/.bashrc' \
    && bash -c 'echo "alias ll=\"ls \$LS_OPTIONS -l\"" >> ~/.bashrc' \
    && bash -c 'echo "export PS1=\"\\[\\e[01;31m\\]\\u@\\h\\[\\e[00m\\]:\\[\\e[01;34m\\]\\w\\[\\e[00m\\]\\$ \"" >> ~/.bashrc' \

# Node.js 24
RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && curl -fsSL https://deb.nodesource.com/setup_24.x | bash - \
    && apt-get install -y --no-install-recommends nodejs \
    && rm -rf /var/lib/apt/lists/*

# Python
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        pipx \
        python3 \
        python3-venv \
        python-is-python3 \
    && rm -rf /var/lib/apt/lists/* \
    && pipx install uv

# Java
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        maven \
        openjdk-21-jdk \
    && rm -rf /var/lib/apt/lists/*

# Rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs \
        | sh -s -- -y --profile default --default-toolchain stable

# Git defaults
RUN git config --global init.defaultBranch main \
    && git config --global core.fileMode false

WORKDIR /workspaces
