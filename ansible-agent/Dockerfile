# --- A N S I B L E ---

# Base image.
FROM agent-base:latest

LABEL maintainer="Viz"

# Install Ansible.
RUN apt-get update && \
    apt-get install -y ansible && \
    apt-get clean

# SSH key.
COPY ./keys/ansible_id_rsa.pub /home/jenkins/.ssh/authorized_keys

# Set correct permissions for SSH (in case authorized_keys is mounted)
RUN chmod 700 /home/jenkins/.ssh && \
    chown -R jenkins:jenkins /home/jenkins/.ssh

# Set working directory
WORKDIR /home/jenkins

# Expose SSH port
EXPOSE 22

# Start SSH daemon
CMD ["/usr/sbin/sshd", "-D"]
