FROM ubuntu:22.10

RUN sed -i 's|archive.ubuntu.com|old-releases.ubuntu.com|g' /etc/apt/sources.list
RUN sed -i 's|security.ubuntu.com|old-releases.ubuntu.com|g' /etc/apt/sources.list
RUN sed -i '/^# deb-src/s/^# //' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install openssh-server openssh-client zlib1g-dev libssl-dev autoconf automake libtool tcpdump -y
RUN apt-get install dpkg-dev --fix-missing -y
RUN apt-get source openssh-client

ENV USER_NAME=prueba
ENV USER_HOME=/home/$USER_NAME

RUN useradd -m -d $USER_HOME $USER_NAME
RUN echo 'prueba:prueba' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
