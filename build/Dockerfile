FROM debian:buster-slim

ARG UPSTREAM_VERSION
ENV DOWNLOAD_URL https://github.com/sigp/lighthouse/releases/download

RUN export ARCH=$(uname -m) && \
    export BINARY=lighthouse-${UPSTREAM_VERSION}-${ARCH}-unknown-linux-gnu-portable.tar.gz && \
    export BINARY_URL=${DOWNLOAD_URL}/${UPSTREAM_VERSION}/${BINARY} && \
    DEBIAN_FRONTEND=noninteractive \
    apt update && apt install --assume-yes --no-install-recommends wget ca-certificates && \
    wget -q $BINARY_URL && \
    tar -xzvf $BINARY && \
    rm -rf $BINARY && \
    cp lighthouse /usr/local/bin/lighthouse && \
    chmod +x /usr/local/bin/lighthouse && \
    rm -rf /var/lib/apt/lists/*

# Verify binary is in correct arch
RUN lighthouse --version

ENTRYPOINT [ "sh", "-c", "exec lighthouse \
    --datadir /data beacon_node \
    --eth1 \
    --http \
    --http-address 0.0.0.0 \
    --http-allow-origin '*' \
    --port 9003 \
    --testnet zinken \
    --eth1-endpoint ${HTTP_WEB3PROVIDER} \
    --max-skip-slots 700 \
    ${EXTRA_OPTS}" ]