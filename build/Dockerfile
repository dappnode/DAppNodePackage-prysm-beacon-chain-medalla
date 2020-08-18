FROM debian:buster-slim

ARG UPSTREAM_VERSION
ENV DOWNLOAD_URL https://github.com/sigp/lighthouse/releases/download
ENV BINARY lighthouse-${UPSTREAM_VERSION}-x86_64-unknown-linux-gnu-portable.tar.gz
ENV BINARY_URL $DOWNLOAD_URL/$UPSTREAM_VERSION/$BINARY

RUN DEBIAN_FRONTEND=noninteractive \
    apt update && apt install --assume-yes --no-install-recommends wget ca-certificates libssl-dev && \
    wget $BINARY_URL && \
    tar -xzvf $BINARY && \
    rm -rf $BINARY && \
    cp lighthouse /usr/local/bin/lighthouse && \
    chmod +x /usr/local/bin/lighthouse && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT [ "sh", "-c", "exec lighthouse --datadir /data beacon_node --eth1 --http --http-address 0.0.0.0 --http-allow-origin '*' --testnet medalla --eth1-endpoint ${HTTP_WEB3PROVIDER} --max-skip-slots 700 ${EXTRA_OPTS}" ]