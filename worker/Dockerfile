# Use the official Ubuntu image as a base
FROM ubuntu:latest

# Avoid prompts from apt.
ENV DEBIAN_FRONTEND=noninteractive

# Update and install SSH server.
RUN apt-get update && \
    apt-get install -y openssh-server sudo && \
    mkdir /var/run/sshd

# Add a new user 'ansibleuser' and set up a password.
RUN useradd -m -s /bin/bash ansibleuser && \
    echo "ansibleuser:ansible" | chpasswd

# Add user to the sudoers
RUN echo 'ansibleuser ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Create ~/.ssh/ directory, add SSH key and fix permissions.
RUN mkdir /home/ansibleuser/.ssh && \
    chmod 700 /home/ansibleuser/.ssh && \
    chown ansibleuser:ansibleuser /home/ansibleuser/.ssh
COPY ./ssh/id_rsa.pub /home/ansibleuser/.ssh/authorized_keys
RUN chown ansibleuser:ansibleuser /home/ansibleuser/.ssh/authorized_keys && \
    chmod 600 /home/ansibleuser/.ssh/authorized_keys

# SSH login fix. Otherwise user is kicked off after login.
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Expose the default SSH port.
EXPOSE 22

# Run the SSH server.
CMD ["/usr/sbin/sshd", "-D"]