FROM ubuntu:22.04

# Базовые утилиты
RUN apt-get update && apt-get install -y \
    curl wget unzip git make python3 python3-pip ssh sudo apt-transport-https gnupg software-properties-common

# Terraform
RUN wget https://releases.hashicorp.com/terraform/1.7.5/terraform_1.7.5_linux_amd64.zip \
    && unzip terraform_1.7.5_linux_amd64.zip \
    && mv terraform /usr/local/bin/ \
    && rm terraform_1.7.5_linux_amd64.zip

# Ansible
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y software-properties-common \
    && apt-add-repository --yes --update ppa:ansible/ansible \
    && apt-get update && apt-get install -y ansible
# kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl" \
    && chmod +x kubectl \
    && mv kubectl /usr/local/bin/

# Helm
RUN curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

# AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install \
    && rm -rf awscliv2.zip aws

# Python packages
RUN pip3 install boto3

# Docker client
RUN apt-get install -y docker.io

# Kind
RUN curl -Lo ./kind "https://kind.sigs.k8s.io/dl/v0.26.0/kind-linux-amd64" \
    && chmod +x ./kind \
    && mv ./kind /usr/local/bin/kind

WORKDIR /workspace
CMD ["/bin/bash"]