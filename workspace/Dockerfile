# Latest centos
FROM centos:7

# System update
RUN yum -y update && yum clean all

# Install devtools
RUN yum install -y vim zsh

# Install essential tools
RUN yum install -y sudo

# Add $USER
ENV user docker
RUN useradd --create-home --home-dir /home/$user --shell /usr/bin/zsh $user
## change password
RUN echo "$user:$user" | chpasswd
## use sudo command without password
RUN echo "$user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Todo: Modify ~/.ssh/config

# Todo: Modify /etc/hosts

# Todo: SSH to $USER@docker.local

