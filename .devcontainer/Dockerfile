FROM python:3.10.5-buster

# Update all,upgrade pip
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y docker bash-completion \
    && pip install --upgrade pip \
    && mkdir /workspace

# Install pip
COPY .devcontainer/requirements.txt /workspace/
RUN if [ -f "requirements.txt" ]; then pip install -r requirements.txt && rm requirements.txt*; fi

# Add kubectl, stern, trivy
ADD https://storage.googleapis.com/kubernetes-release/release/v1.24.3/bin/linux/amd64/kubectl /usr/local/bin/kubectl
ADD https://github.com/wercker/stern/releases/download/1.11.0/stern_linux_amd64 /usr/local/bin/stern
RUN chmod +x ./usr/local/bin/kubectl \
    && kubectl version --client
    && chmod +x ./usr/local/bin/stern \
    && stern --version
    && wget -q -O /tmp/trivy.deb https://github.com/aquasecurity/trivy/releases/download/v0.30.4/trivy_0.30.4_Linux-64bit.deb \
    && dpkg -i /tmp/trivy.deb \
    && rm /tmp/trivy.deb
    && trivy --version

# Add auto completer & alias
ADD .bashrc /tmp/
RUN cat /tmp/.bashrc >> /root/.bashrc

# Copy k8s config
COPY ./kube-config/config /root/.kube/

WORKDIR /workspace
