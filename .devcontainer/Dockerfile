# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.148.1/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version: bionic, focal
ARG UBUNTU_VERSION="20.04"
FROM ubuntu:${UBUNTU_VERSION}

ARG PYTHON_VERSION=3.8

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get -y install git unzip vim \
    azure-cli curl zsh gnupg2 iputils-ping jq software-properties-common \
    # Clean up
    && rm -rf /tmp/docker-downloads \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Install Python
RUN apt-get update \
    && apt-get -y install python${PYTHON_VERSION} python3-pip \
       build-essential libssl-dev libffi-dev python-dev \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3 1 \
    && update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1

# Install docker
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get install -y docker-ce docker-ce-cli containerd.io

ARG DEBIAN_FRONTEND=interactive
