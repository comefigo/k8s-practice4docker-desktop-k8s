FROM python:3.10.5-buster

# Update all,upgrade pip
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y docker bash-completion vim \
    && pip install --upgrade pip \
    && mkdir /workspace

# Install pip
COPY .devcontainer/requirements.txt /workspace/
RUN if [ -f "requirements.txt" ]; then pip install -r requirements.txt && rm requirements.txt*; fi

# Add kubectl, stern
ADD https://storage.googleapis.com/kubernetes-release/release/v1.24.3/bin/linux/amd64/kubectl /usr/local/bin/kubectl

RUN wget -q -O /tmp/stern.tar.gz https://github.com/stern/stern/releases/download/v1.22.0/stern_1.22.0_linux_amd64.tar.gz \
    && tar -zxvf /tmp/stern.tar.gz -C /tmp/ \
    && cp /tmp/stern /usr/local/bin/stern \
    && chmod +x /usr/local/bin/kubectl \
    && kubectl version --client \
    && chmod +x /usr/local/bin/stern \
    && stern --version

# Add trivy
RUN wget -q -O /tmp/trivy.deb https://github.com/aquasecurity/trivy/releases/download/v0.31.1/trivy_0.31.1_Linux-64bit.deb \
    && dpkg -i /tmp/trivy.deb \
    && rm -f /tmp/trivy.deb \
    && trivy --version

# Add helm
RUN mkdir /tmp/helm \
    && wget -q -O /tmp/helm/helm.tar.gz https://get.helm.sh/helm-v3.9.2-linux-amd64.tar.gz \
    && tar -zxvf /tmp/helm/helm.tar.gz -C /tmp/helm/ \
    && chmod +x /tmp/helm/linux-amd64/helm \
    && mv /tmp/helm/linux-amd64/helm /usr/local/bin/helm \
    && helm version \
    && rm -rf /tmp/helm

# Add auto completer & alias
ADD .bashrc /tmp/
RUN cat /tmp/.bashrc >> /root/.bashrc

# Copy k8s config
COPY ./kube-config/config /root/.kube/
RUN chmod 600 -R /root/.kube/

WORKDIR /workspace
