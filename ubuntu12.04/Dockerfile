# Dockerfile for building Ansible image for Ubuntu 12.04 (presice), with as few additional software as possible.
#
# @see https://launchpad.net/~ansible/+archive/ubuntu/ansible
#
# Version  1.0
#


# pull base image
FROM ubuntu:12.04

MAINTAINER William Yeh <william.pjyeh@gmail.com>


RUN echo "===> Adding Ansible's PPA..."  && \
    echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu precise main" | tee /etc/apt/sources.list.d/ansible.list           && \
    echo "deb-src http://ppa.launchpad.net/ansible/ansible/ubuntu precise main" | tee -a /etc/apt/sources.list.d/ansible.list    && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 7BB9C367    && \
    DEBIAN_FRONTEND=noninteractive  apt-get update  && \
    \
    \
    echo "===> Installing Ansible (and sudo)..."  && \
    apt-get install -y ansible sudo && \
    \
    \
    echo "===> Removing Ansible PPA..."  && \
    rm -rf /var/lib/apt/lists/*  /etc/apt/sources.list.d/ansible.list  && \
    \
    \
    echo "===> Adding hosts for convenience..."  && \
    echo 'localhost' > /etc/ansible/hosts


# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]
