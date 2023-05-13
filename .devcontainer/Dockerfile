FROM ubuntu:latest
WORKDIR /tmp
# Prerequisites for installs:
RUN apt update && apt upgrade -y

# Install AWS CLI
RUN apt install curl zip -y
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install

# Install kubectl
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/arm64/kubectl"
RUN install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
RUN kubectl version --client
# RUN kubectl completion bash | tee /etc/bash_completion.d/kubectl > /dev/null
# RUN chmod a+r /etc/bash_completion.d/kubectl

# Install terraform cli
RUN apt install -y gnupg software-properties-common wget
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list
RUN apt update
RUN apt install terraform -y

# EKS Blueprints for Terraform
RUN apt install -y jq gettext bash-completion moreutils

# Useful
RUN apt install git -y

# Make sure all is up to date
RUN apt update && apt upgrade -y
