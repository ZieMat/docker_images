FROM ubuntu:24.04




# Install python3 and pip3
RUN apt-get update && apt-get install -y \ 
    python3 \
    python3-pip

#Extract Ubuntu version from base image

# ARG VERSION_ID
# RUN echo $(cat /etc/os-release | grep VERSION_ID | cut -d'"' -f2) > /tmp/version && \
#     export VERSION_ID=$(cat /tmp/version)


# PowerShell

## Pre-requisite packages
RUN apt-get update && apt-get install -y \
    wget apt-transport-https software-properties-common

## Download the Microsoft repository GPG keys
RUN wget -q https://packages.microsoft.com/config/ubuntu/24.04/packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    rm packages-microsoft-prod.deb

## Install PowerShell
RUN apt-get update && apt-get install -y \
    powershell && \
    rm -rf /var/lib/apt/lists/*

CMD ["bin/bash"]