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

# Build fresh Spigot jars
RUN mkdir -p /opt/buildtools
RUN curl -o /opt/buildtools/BuildTools.jar https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
RUN cd /opt/buildtools; java -jar BuildTools.jar

# Setup Minecraft server
RUN cd /
RUN mkdir -p /srv/res
RUN cp /opt/buildtools/spigot-*.jar /srv/res/spigot.jar

ADD ./start /srv/res/start
ADD ./server.properties /srv/res/server.properties	
ADD ./spigot.jar /srv/res/spigot.jar
RUN chmod a+x /srv/res/start

# Expose service port
EXPOSE 25565

# Provide data directory

VOLUME "/srv/server"

CMD "/srv/res/start"

