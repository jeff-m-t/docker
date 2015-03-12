FROM java:7
MAINTAINER Jeff Thompson <jeff.m.t@gmail.com>

RUN apt-get update && apt-get install -y apt-transport-https && apt-get install -y emacs-nox

RUN echo "deb https://dl.bintray.com/sbt/debian /" > /etc/apt/sources.list.d/sbt.list
RUN apt-get update && apt-get install --force-yes -y sbt
