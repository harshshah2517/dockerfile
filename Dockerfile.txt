FROM ubuntu:16.04
USER root

RUN apt-get update
RUN apt-get -y install software-properties-common net-tools wget curl nano \
    sudo gcc make automake git dpkg-dev build-essential iputils-ping

COPY ./src/packages.sh /etc
RUN /etc/packages.sh

RUN export DEBIAN_FRONTEND=noninteractive && apt-get -y install xfce4
RUN apt-get install dialog && apt-get -y install xfce4-goodies

RUN apt-get -y install tightvncserver
ENV USER=root
COPY ./src/vncserver.py /etc/
RUN  /etc/vncserver.py

CMD  vncserver && sleep infinity

