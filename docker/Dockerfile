FROM docker.io/danthomson/devenv:base
MAINTAINER Daniel Thomson DanielOliverThomson@gmail.com

# Improve sshd security
COPY config/container/sshd_config /etc/ssh/sshd_config.d/authentication.conf

# Setup user that will be doing development
RUN useradd -ms /bin/bash developer
RUN mkdir /home/developer/.ssh
COPY config/container/authorized_keys /home/developer/.ssh/
RUN chown --recursive developer:developer /home/developer

ENTRYPOINT ["/usr/sbin/sshd", "-D"]
