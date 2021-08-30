FROM docker.io/debian:latest
MAINTAINER Daniel Thomson DanielOliverThomson@gmail.com

RUN apt update
RUN apt -y upgrade
RUN apt install -y openssh-server
RUN apt install -y tmux
RUN apt install -y vim

# This directory is required by sshd
RUN mkdir /run/sshd
