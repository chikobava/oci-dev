FROM ubuntu:20.04

# Create a user for development
ARG USERNAME=oracle
ARG UID=1000
# Sets noninteractive for apt-get
ARG DEBIAN_FRONTEND=noninteractive

# Install required software
RUN apt-get update && \
    apt-get install -y sudo git curl wget python3 lsb-release gpg software-properties-common && \
    echo "deb https://apt.releases.hashicorp.com $(lsb_release -cs) main" >  /etc/apt/sources.list.d/hashicorp.list && \
    curl https://apt.releases.hashicorp.com/gpg | apt-key add && \
    apt-get update && \
    add-apt-repository --yes --update ppa:ansible/ansible && \
    apt-get install -y packer ansible terraform && \
    groupadd -g $UID $USERNAME && \
    useradd -u $UID -g $UID -m $USERNAME -s /bin/bash && \
    usermod -aG sudo $USERNAME && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME 

# Install oc
USER oracle
RUN cd && \
    packer plugins install github.com/hashicorp/oracle && \
    wget https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh && \
    chmod +x ./install.sh && \
    ./install.sh --accept-all-defaults

WORKDIR /oc