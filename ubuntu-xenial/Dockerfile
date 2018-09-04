FROM ubuntu:xenial
# 14.04 - trusty
# 16.04 - xenial
# 18.04 - bionic
# 18.10 - cosmic

MAINTAINER Yi-Soo An <yisooan@gmail.com>

# Replace the repo with kakao mirror
# Consider uncommenting for Korea
# RUN sed -i "s/archive.ubuntu.com/mirror.kakao.com/g" /etc/apt/sources.list

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y git sudo vim-common

# Add an user named webos
RUN useradd -m webos

# Add sudo permission
RUN touch /etc/sudoers.d/webos
RUN echo "webos ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/webos

USER webos
WORKDIR /home/webos

RUN mkdir mpoint
WORKDIR /home/webos/mpoint

