# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory
WORKDIR /usr/src/app

ENV ANSIBLE_HOST_KEY_CHECKING=False

# Install system dependencies including SSH client
RUN apt-get update && \
    apt-get install -y ssh-client && \
    rm -rf /var/lib/apt/lists/*

# Install Ansible via pip
RUN pip install ansible

# Copy your Ansible configurations and playbooks into the container
# COPY ./ansible /usr/src/app/ansible

# Copy SSH keys (assuming keys are stored in ansible/ssh_keys directory within your project)
COPY ansible/ssh_keys/id_rsa /root/.ssh/id_rsa
COPY ansible/ssh_keys/id_rsa.pub /root/.ssh/id_rsa.pub

# Correct file permissions for SSH keys
RUN chmod 600 /root/.ssh/id_rsa && chmod 644 /root/.ssh/id_rsa.pub

# Keep the container running
CMD ["sleep", "infinity"]