FROM jenkins/ssh-agent:6.19.0-jdk17
ENV DEBIAN_FRONTEND noninteractive
USER root
RUN apt-get update \ 
    && apt-get install -y \
    curl wget git python3 python3-pip python3-venv unzip ansible nano # Versioning to be included
    
COPY requirements.txt ./requirements.txt

# Configure venv for Python linting tools 
RUN python3 -m venv /opt/python-lint\
    && . /opt/python-lint/bin/activate \
    && pip install -r requirements.txt \ 
    && rm requirements.txt
    
# Install Trivy
RUN echo "INSTALLING TRIVY" \
    && wget https://github.com/aquasecurity/trivy/releases/download/v0.64.1/trivy_0.64.1_Linux-64bit.deb \
    && dpkg -i trivy_0.64.1_Linux-64bit.deb \
    && rm trivy_0.64.1_Linux-64bit.deb \
    && trivy --version

# Group ID is taken from the group ID set on host.
RUN groupadd -g 984 docker && \
    usermod -aG docker jenkins

RUN curl -fsSL https://get.docker.com/ | sh
RUN curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose

#USER jenkins