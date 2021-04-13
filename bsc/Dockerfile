FROM ubuntu:xenial

# Path to the zip of the release
ARG RELEASE_URL

# install tools and dependencies
RUN set -eux \
    && apt-get update \
    && apt-get install -y --no-install-recommends file curl jq ca-certificates wget unzip \
    && apt-get autoremove -y \
    && apt-get clean \
    && update-ca-certificates \
    && rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* \
    && cd /usr/local/bin \
    && wget -qO geth "$RELEASE_URL" \
    && chmod +x ./geth \
    && mkdir /blockchain \
    && mkdir /blockchain/data \
    && mkdir /blockchain/keys

WORKDIR /root

EXPOSE 8545 8546 8557

ENTRYPOINT ["geth"]
