# Dockerfile for building Ansible image from source for Ubuntu 16.04 (Xenial), with as few additional software as possible.
#
# @see http://docs.ansible.com/ansible/intro_installation.html#running-from-source
#
# Version  1.0
#


# pull base image
FROM ubuntu:16.04

MAINTAINER William Yeh <william.pjyeh@gmail.com>


RUN echo "===> Adding Ansible's prerequisites..."   && \
    apt-get update -y            && \
    DEBIAN_FRONTEND=noninteractive  \
        apt-get install --no-install-recommends -y -q  \
                build-essential                        \
                python-pip python-dev python-yaml      \
                libffi-dev libssl-dev                  \
                libxml2-dev libxslt1-dev zlib1g-dev    \
                git                                 && \
    pip install --upgrade wheel setuptools          && \
    pip install --upgrade pyyaml jinja2 pycrypto    && \
    \
    \
    echo "===> Downloading Ansible's source tree..."            && \
    git clone git://github.com/ansible/ansible.git --recursive  && \
    \
    \
    echo "===> Compiling Ansible..."      && \
    cd ansible                            && \
    bash -c 'source ./hacking/env-setup'  && \
    \
    \
    echo "===> Moving useful Ansible stuff to /opt/ansible ..."  && \
    mkdir -p /opt/ansible                && \
    mv /ansible/bin   /opt/ansible/bin   && \
    mv /ansible/lib   /opt/ansible/lib   && \
    mv /ansible/docs  /opt/ansible/docs  && \
    rm -rf /ansible                      && \
    \
    \
    echo "===> Clean up..."                                         && \
    apt-get remove -y --auto-remove \
            build-essential python-pip python-dev git libffi-dev libssl-dev  && \
    apt-get clean                                                   && \
    rm -rf /var/lib/apt/lists/*                                     && \
    \
    \
    echo "===> Adding hosts for convenience..."  && \
    mkdir -p /etc/ansible                        && \
    echo 'localhost' > /etc/ansible/hosts


ENV PATH        /opt/ansible/bin:$PATH
ENV PYTHONPATH  /opt/ansible/lib:$PYTHONPATH
ENV MANPATH     /opt/ansible/docs/man:$MANPATH

# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]
