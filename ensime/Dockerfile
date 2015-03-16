FROM java:8
MAINTAINER Jeff Thompson <jeff.m.t@gmail.com>

RUN useradd -ms /bin/bash developer

RUN apt-get update && apt-get install -y apt-transport-https && apt-get install -y emacs-nox

RUN echo "deb https://dl.bintray.com/sbt/debian /" > /etc/apt/sources.list.d/sbt.list
RUN apt-get update && apt-get install --force-yes -y sbt

ENV HOME /home/developer
USER developer
WORKDIR /home/developer

ADD emacs-pkg* /home/developer/
ADD dotemacs /home/developer/.emacs

RUN ./emacs-pkg-install.sh ensime && \
    rm emacs-pkg*

ADD dotsbt /home/developer/.sbt-bootstrap

RUN mkdir /home/developer/source && \
    echo "\n# Ensure developemtn environment is configured" >> /home/developer/.bashrc && \
    echo 'if [ ! -d ~/source/.sbt ]; then echo "Bootstraping" && cp -r ~/.sbt-bootstrap ~/source/.sbt; fi' >> /home/developer/.bashrc && \
    echo 'alias sbt="sbt -sbt-dir ~/source/.sbt -ivy ~/source/.ivy2"' >> /home/developer/.bashrc && \
    echo 'if [ -f ~/source/.bashrc ]; then . ~/source/.bashrc; fi' >> /home/developer/.bashrc
    

USER root
RUN chown -R developer.developer /home/developer

USER developer










