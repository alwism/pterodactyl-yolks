FROM    --platform=$TARGETOS/$TARGETARCH alpine:3.17
LABEL   author="Alwism" maintainer="60648387+alwism@users.noreply.github.com"

RUN     adduser -D --home /home/container container

# Install prerequisites
RUN     apk update \
        && apk add --no-cache \
          bash \
          gcc \
          g++ \
          curl \
          libgcc \
          libcurl \
          libssl3 \
        && rm -rf /var/cache/apk/*

# install steamcmd
RUN     mkdir -p "/tmp/steamcmd" && cd /tmp/steamcmd \
        && curl -sSL https://media.steampowered.com/installer/steamcmd_linux.tar.gz > steamcmd.tar.gz \
        && tar xvf steamcmd.tar.gz && rm steamcmd.tar.gz \
        && mv /tmp/steamcmd/ /home/container/steamcmd/

## install rcon
RUN     cd /tmp/ \
        && curl -sSL https://github.com/gorcon/rcon-cli/releases/download/v0.10.2/rcon-0.10.2-amd64_linux.tar.gz > rcon.tar.gz \
        && tar xvf rcon.tar.gz && rm rcon.tar.gz \
        && mv rcon-0.10.2-amd64_linux/rcon /usr/local/bin/

USER    container
ENV     USER=container HOME=/home/container
WORKDIR /home/container

#RUN     steamcmd +quit

COPY    entrypoint.sh /entrypoint.sh
CMD     [ "/bin/bash", "/entrypoint.sh" ]
