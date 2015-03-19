FROM java:8
MAINTAINER Jeff Thompson <jeff.m.t@gmail.com>

RUN useradd -ms /bin/bash developer && echo 'developer:developer' | chpasswd && adduser developer sudo

RUN apt-get update && apt-get install -y apt-transport-https && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9 && \
    echo deb https://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list

RUN apt-get update && \
    apt-get install -y emacs-nox git less lxc-docker sudo

ENV HOME /home/developer
USER developer
WORKDIR /home/developer
 
ADD emacs-pkg* /home/developer/
ADD dotemacs /home/developer/.emacs-bootstrap
RUN mkdir ./.emacs.d-bootstrap && \
    ln -s ./.emacs-bootstrap ./.emacs && \
    ln -s ./.emacs.d-bootstrap ./.emacs.d

RUN ./emacs-pkg-install.sh ensime && \
    rm emacs-pkg*

ADD bin /home/developer/bin
ADD https://repo.typesafe.com/typesafe/ivy-releases/org.scala-sbt/sbt-launch/0.13.7/sbt-launch.jar /home/developer/bin/sbt-launch.jar
ADD dotsbt /home/developer/.sbt-bootstrap

RUN mkdir /home/developer/source && \
    echo "\n# Ensure developemtn environment is configured" >> /home/developer/.bashrc && \
    echo 'if [ ! -f ~/source/.emacs ]; then echo "Bootstraping Emacs" && cp ~/.emacs-bootstrap ~/source/.emacs; ln -sf ~/source/.emacs ~/.emacs; fi' >> /home/developer/.bashrc && \
    echo 'if [ ! -d ~/source/.emacs.d ]; then echo "Bootstraping Emacs.d" && cp -r ~/.emacs.d-bootstrap ~/source/.emacs.d; rm ~/.emacs.d && ln -sf ~/source/.emacs.d ~/.emacs.d; fi' >> /home/developer/.bashrc && \
    echo 'if [ ! -d ~/source/.sbt ]; then echo "Bootstraping SBT" && cp -r ~/.sbt-bootstrap ~/source/.sbt; ln -s ~/source/.sbt ~/.sbt; fi' >> /home/developer/.bashrc && \
    echo 'if [ ! -d ~/source/.ivy2 ]; then echo "Bootstraping Ivy" && mkdir ~/source/.ivy2; ln -s ~/source/.ivy2 ~/.ivy2; fi' >> /home/developer/.bashrc && \
    echo 'export PATH=~/bin:$PATH' >> /home/developer/.bashrc && \
    echo 'if [ -f ~/source/.bashrc ]; then . ~/source/.bashrc; fi' >> /home/developer/.bashrc
        
ADD test-ensime /home/developer/source/test-ensime

USER root
RUN chown -R developer.developer /home/developer

USER developer










