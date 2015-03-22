FROM java:8
MAINTAINER Jeff Thompson <jeff.m.t@gmail.com>

RUN useradd -ms /bin/bash dev && echo 'dev:dev' | chpasswd && adduser dev sudo

RUN apt-get update && apt-get install -y apt-transport-https && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9 && \
    echo deb https://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list

RUN apt-get update && \
    apt-get install -y emacs-nox git less lxc-docker sudo

ENV HOME /home/dev
USER dev
WORKDIR /home/dev
 
ADD emacs-pkg* /home/dev/
ADD dotemacs /home/dev/.emacs
RUN mkdir ./.emacs.d

RUN ./emacs-pkg-install.sh ensime && rm emacs-pkg*

ADD dotsbt /home/dev/.sbt
ADD bin /home/dev/bin

RUN mkdir /home/dev/work && echo 'export PATH=~/bin:$PATH' >> /home/dev/.bashrc
        
ADD test-ensime /home/developer/source/test-ensime

USER root
RUN chown -R dev.dev /home/dev

USER dev

VOLUME /home/dev

CMD /bin/bash









