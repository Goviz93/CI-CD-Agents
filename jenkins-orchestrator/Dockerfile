# Use the official Jenkins LTS base image
FROM jenkins/jenkins

LABEL maintainer="Viz"

# Switch to root to install packages and copy configs
USER root

# Install sudo (optional, useful for testing scripts in pipelines)
RUN apt-get update && \
    apt-get install -y sudo && \
    echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

# Install plugins from plugins.txt
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt

# Copy JCasC YAML configuration
COPY config-as-code/ /var/jenkins_home/config-as-code/

# Install basic tools.
RUN apt-get update && \
    apt-get install -y iputils-ping iproute2 dnsutils net-tools curl && \
    apt-get clean


# Set environment variable to tell Jenkins where to find JCasC config
ENV CASC_JENKINS_CONFIG=/var/jenkins_home/config-as-code/jenkins.yaml

# Switch back to Jenkins user
USER jenkins

