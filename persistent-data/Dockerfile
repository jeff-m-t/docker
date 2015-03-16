FROM java:8
MAINTAINER Jeff Thompson <jeff.m.t@gmail.com>

RUN useradd -ms /bin/bash developer

RUN mkdir -p /home/developer/source && \
    chown -R developer:developer /home/developer/source

VOLUME /home/developer/source

USER developer

CMD ["echo", "Data Container for Development Sources"]

