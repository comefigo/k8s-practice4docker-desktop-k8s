FROM python:3.10.5-buster

# Add kubectl
ADD https://storage.googleapis.com/kubernetes-release/release/v1.24.3/bin/linux/amd64/kubectl /usr/local/bin/kubectl

# Update all,upgrade pip
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y docker bash-completion \
    && pip install --upgrade pip \
    && mkdir /workspace \
    && chmod +x ./usr/local/bin/kubectl

# Install pip
COPY .devcontainer/requirements.txt /workspace/
RUN if [ -f "requirements.txt" ]; then pip install -r requirements.txt && rm requirements.txt*; fi

# Add auto completer & alias
ADD .bashrc /tmp/
RUN cat /tmp/.bashrc >> /root/.bashrc

# Copy k8s config
COPY ./kube-config/config /root/.kube/

WORKDIR /workspace
