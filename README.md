# Minimal XMage Server based on Alpine

[![](https://badge.imagelayers.io/goesta/xmage-alpine:latest.svg)](https://imagelayers.io/?images=goesta/xmage-alpine:latest)

## Usage
    docker run --rm -it \
        -p 17171:17171 \
        -p 17179:17179 \
        -e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
        -e "XMAGE_DOCKER_AUTHENTICATION_ACTIVATED=false"\
        -e "XMAGE_DOCKER_SERVER_NAME=xmage-server" \
        flippyboy/xmage-alpine


Using the `XMAGE_*` environment variables you can modify the `config.xml` file.
We no longer need to use the `--add-host` option as this is handled by the startup script.

You can limit the memory and CPU shares using the `-m` and `-c` options.   
For more informations on this topic  see: https://docs.docker.com/engine/reference/run/#runtime-constraints-on-resources

    docker run --rm -it \
        -p 17171:17171 \
        -p 17179:17179 \
        -m 2g
        -c 512
        -e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
        -e "XMAGE_DOCKER_SERVER_NAME=xmage-server" \
        flippyboy/xmage
        
        
## Deploy in Azure

