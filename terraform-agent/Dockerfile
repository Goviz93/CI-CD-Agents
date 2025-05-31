# --- T E R R A F O R M ---

# Base image with SSH, sudo, and Jenkins user
FROM agent-base:latest

LABEL maintainer="Viz"

# Install Terraform CLI
RUN apt-get update && \
    apt-get install -y curl unzip && \
    curl -fsSL https://releases.hashicorp.com/terraform/1.6.6/terraform_1.6.6_linux_amd64.zip -o terraform.zip && \
    unzip terraform.zip && mv terraform /usr/local/bin/terraform && rm terraform.zip

# Install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && ./aws/install && rm -rf awscliv2.zip aws

# SSH key.
COPY ./keys/terraform_id_rsa.pub /home/jenkins/.ssh/authorized_keys

# Set correct permissions for SSH (in case authorized_keys is mounted)
RUN chmod 700 /home/jenkins/.ssh && \
    chown -R jenkins:jenkins /home/jenkins/.ssh

# Set working directory
WORKDIR /home/jenkins

# Expose SSH port
EXPOSE 22

# Start SSH daemon
CMD ["/usr/sbin/sshd", "-D"]

