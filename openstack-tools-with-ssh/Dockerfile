# Docker container with OpenStack client + SSH server for remote access

FROM ubuntu:latest
LABEL maintainer "lrivallain@sii.fr"

RUN apt-get update && apt-get upgrade -qqy && \
    apt-get install -qqy build-essential wget python-dev python-pip vim jq curl && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install --no-cache-dir --upgrade pip setuptools python-openstackclient

RUN apt-get update && \
apt-get install -y --no-install-recommends openssh-server && \
rm -rf /var/lib/apt/lists/*

RUN mkdir /var/run/sshd
RUN echo 'root:ostools@' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
