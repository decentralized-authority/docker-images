FROM ubuntu:18.04 as prep
LABEL MAINTAINER="leopere [at] nixc [dot] us"
## TODO: Implement version pinning. `apt-get install curl=<version>`
RUN apt-get update && \
  apt-get -y install unzip curl build-essential && \
  apt-get autoclean -y && \
  rm -rf /var/lib/apt/lists/*
WORKDIR /
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
COPY ./stuff/start.sh start
COPY ./stuff/healthcheck.sh healthcheck
COPY ./stuff/advance_blocks.sh advance
COPY ./stuff/fix-permissions.c fix-permissions.c
ARG release_url
# require that release_url is set
RUN test -n "$release_url"
RUN curl --progress-bar -L -o ./lbrycrd-linux.zip "$release_url" && \
  unzip ./lbrycrd-linux.zip && \
  gcc fix-permissions.c -o fix-permissions && \
  chmod +x ./lbrycrdd ./lbrycrd-cli ./lbrycrd-tx ./start ./healthcheck ./fix-permissions ./advance

FROM ubuntu:18.04 as app
COPY --from=prep /lbrycrdd /lbrycrd-cli /lbrycrd-tx /start /healthcheck /fix-permissions /advance /usr/bin/
RUN mkdir /lbry
RUN mkdir /lbry/data
RUN mkdir /lbry/keys
RUN apt-get update && apt-get -y install wget && apt-get autoclean -y && rm -rf /var/lib/apt/lists/*
VOLUME ["/lbry"]
WORKDIR /lbry
HEALTHCHECK CMD /usr/bin/healthcheck
EXPOSE 9246 9245 11337 29245

entrypoint ["/usr/bin/lbrycrdd"]
