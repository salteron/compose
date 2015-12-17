FROM ubuntu:trusty

# Ignore configuration requests
ENV DEBIAN_FRONTEND noninteractive

# ensure UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

# YEKT locale
RUN mv /etc/localtime /etc/localtime-old
RUN ln -sf /usr/share/zoneinfo/Asia/Yekaterinburg /etc/localtime

# add apt repositories
RUN apt-get update
RUN apt-get -y -q upgrade

RUN apt-get -y -q install vim ssh

# create init script
RUN touch /root/init.sh
RUN echo "#!/bin/sh" >> /root/init.sh
RUN echo "set -x" >> /root/init.sh
RUN chmod +x /root/init.sh
