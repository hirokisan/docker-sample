# latest centos
FROM centos:7

# system update
RUN yum -y update && yum clean all

# install devtools
RUN yum install -y vim zsh

# install essential tools
RUN yum install -y sudo

# Todo: Add $USER
ENV user docker
RUN useradd --create-home --home-dir /home/$user --shell /usr/bin/zsh $user

# Todo: Modify ~/.ssh/config

# Todo: Modify /etc/hosts

# Todo: SSH to $USER@docker.local

