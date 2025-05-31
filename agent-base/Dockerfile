FROM ubuntu:22.04

#To avoid dialog windows.
ENV DEBIAN_FRONTEND=noninteractive

# Install essential tools and dependencies
RUN apt-get update && apt-get install -y \
    iputils-ping \
    iproute2 \
    net-tools \
    vim \
    curl \
    wget \
    unzip \
    git \
    sudo \
    gnupg \
    software-properties-common \
    ca-certificates \
    lsb-release \
    apt-transport-https \
    openjdk-17-jdk \
    openssh-server && \
    apt-get clean

# Create the "jenkins" user with sudo privileges
RUN useradd -m -s /bin/bash jenkins && \
    echo 'jenkins ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers && \
    mkdir -p /home/jenkins/.ssh && \
    chown -R jenkins:jenkins /home/jenkins/.ssh && \
    chmod 700 /home/jenkins/.ssh

# Prepare SSH service
RUN mkdir -p /var/run/sshd

# Expose SSH port
EXPOSE 22

# Default command to start SSH
CMD ["/usr/sbin/sshd", "-D"]

