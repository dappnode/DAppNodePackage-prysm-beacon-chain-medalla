FROM sigp/lighthouse:latest

RUN apt update && \
    apt install -y ca-certificates && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT [ "sh", "-c", "exec lighthouse --datadir /data beacon_node --eth1 --http --http-address 0.0.0.0 --http-allow-origin '*' --testnet medalla --eth1-endpoint ${HTTP_WEB3PROVIDER} ${EXTRA_OPTS}" ]