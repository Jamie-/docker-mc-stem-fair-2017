# Spigot Minecraft server Dockerfile

# Use Debian Jessie as base
FROM debian:jessie
MAINTAINER Jamie Scott

# Install prerequisits
RUN apt-get update
RUN apt-get install curl git -y
RUN curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u121-b13/e9e7ea248e2c4826b92b3f075a80e441/jdk-8u121-linux-x64.tar.gz > /tmp/jdk.tar.gz
RUN tar -zxf /tmp/jdk.tar.gz -C /opt
RUN mv /opt/jdk* /opt/java
RUN ln -s /opt/java/bin/java /usr/bin/java

# Setup Minecraft server
RUN cd /
RUN mkdir -p /srv/res
ADD ./start /srv/res/start
ADD ./ops.json /srv/res/ops.json
ADD ./spigot.jar /srv/res/spigot.jar
RUN chmod a+x /srv/res/start

# Expose service port
EXPOSE 25565

# Provide data directory

VOLUME "/srv/server"

CMD "/srv/res/start"

