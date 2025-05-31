# --- T E S T  T O O L S  -  P Y T H O N ---

FROM agent-base:latest

LABEL maintainer="Viz"

# Install Python and testing tools
RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip3 install --upgrade pip && \
    pip3 install \
        pytest \
        coverage \
        flake8 \
        bandit && \
    apt-get clean

# Install SonarScanner
ENV SONAR_SCANNER_VERSION=5.0.1.3006
ENV SONAR_SCANNER_HOME=/opt/sonar-scanner

RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip && \
    unzip sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip && \
    mv sonar-scanner-${SONAR_SCANNER_VERSION}-linux ${SONAR_SCANNER_HOME} && \
    rm sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip

ENV PATH="${SONAR_SCANNER_HOME}/bin:${PATH}"

# SSH key.
COPY ./keys/test_id_rsa.pub /home/jenkins/.ssh/authorized_keys

# Set permissions for SSH.
RUN chmod 700 /home/jenkins/.ssh && \
    chmod 600 /home/jenkins/.ssh/authorized_keys && \
    chown -R jenkins:jenkins /home/jenkins/.ssh

# Set working directory
WORKDIR /home/jenkins

# Expone puerto SSH
EXPOSE 22

# Inicia el servicio SSH
CMD ["/usr/sbin/sshd", "-D"]
