# Latest centos
FROM centos:7

#### Enable systemd ####
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/sbin/init"]

########################

#### Install tools ####

# System update
RUN yum -y update

# Install devtools
RUN yum install -y vim zsh git curl

# Install build essential tools
RUN yum install -y gcc gcc-c++ kernel-devel make

# Install sudo
RUN yum install -y sudo

# Install firewalld (if install firewalld and want to use git or connect to network, need to modify configure)
#RUN yum -y install firewalld

# Install NetworkManager
#RUN yum -y install NetworkManager

# Install sshd
RUN yum -y install openssh-server

# Clean cache
RUN yum clean all

#######################

#### Add user ####

# Add $USER
ENV user docker
RUN useradd --create-home --home-dir /home/$user --shell /usr/bin/zsh $user
## change password
RUN echo "$user:$user" | chpasswd
## use sudo command without password
RUN echo "$user ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

##################

#### Enable SSH ####

USER $user
## copy key
RUN mkdir -m 0700 -p ~/.ssh
COPY ./id_rsa     /home/$user/.ssh/id_rsa
COPY ./id_rsa.pub /home/$user/.ssh/authorized_keys
RUN sudo chown -R $user:$user ~/.ssh
RUN chmod -R 0700 ~/.ssh
RUN chmod -R 0600 ~/.ssh/*
## change config file
USER root
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config
## avoid slow ssh https://www.serverpronto.com/accounts/knowledgebase.php?action=displayarticle&id=16&language=german
RUN sed -i 's/#UseDNS yes/UseDNS no/g' /etc/ssh/sshd_config

## Expose ports
EXPOSE 22

####################

#### Install dotfiles ####

USER $user
RUN git clone https://github.com/hirokisan/dotfiles.git ~/dotfiles
USER root

##########################
