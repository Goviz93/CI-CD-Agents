# --- D O C K E R ---

# Base image.
FROM agent-base:latest

LABEL maintainer="Viz"

# Install docker-cli.
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker.gpg && \
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" \
    > /etc/apt/sources.list.d/docker.list && \
    apt-get update && \
    apt-get install -y docker-ce-cli && \
    apt-get clean

# SSH key.
COPY ./keys/docker_id_rsa.pub /home/jenkins/.ssh/authorized_keys

# Set correct permissions for SSH (in case authorized_keys is mounted)
RUN chmod 700 /home/jenkins/.ssh && \
    chown -R jenkins:jenkins /home/jenkins/.ssh

# Set working directory
WORKDIR /home/jenkins

# Create docker group.
RUN groupadd -g 1001 docker && \
    usermod -aG docker jenkins

# Expose SSH port
EXPOSE 22

# Start SSH daemon
CMD ["/usr/sbin/sshd", "-D"]
