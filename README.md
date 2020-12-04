# Minimal XMage Server based on Alpine

[![](https://badge.imagelayers.io/goesta/xmage-alpine:latest.svg)](https://imagelayers.io/?images=goesta/xmage-alpine:latest)

## Usage
    docker run --rm -it \
        -p 17171:17171 \
        -p 17179:17179 \
        -e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
        -e "XMAGE_DOCKER_AUTHENTICATION_ACTIVATED=false"\
        -e "XMAGE_DOCKER_SERVER_NAME=xmage-server" \
        rpgdude/xmage-alpine


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
        rpgdude/xmage
        
        
## Deploy in Azure

It is easy to run this container using Azure Container Instances.
Examples using Azure Shell:

You need a resource group for your deployment. If you don't already have one, create one using the shell.
    
    az group create --name myResourceGroup --location eastus
    
Make note of the location. This is used for your FQDN later.
Deploy your container:

    az container create \
    -g myResourceGroup \
    --name xmage \
    --image rpgdude/xmage-alpine \
    --ports 17171 17179 \
    --dns-name-label examplexmageserver \
    --cpu 1 \
    --memory 2 \
    --environment-variables XMAGE_DOCKER_SERVER_ADDRESS=examplexmageserver.eastus.azurecontainer.io XMAGE_DOCKER_SERVER_NAME=xmage-server XMAGE_DOCKER_AUTHENTICATION_ACTIVATED=false
    
`-g` should be the same resource group you created earlier  
`--name` is what your resource in Azure will be named   
`--dns-name-label` must be a unique name for your region    
`XMAGE_DOCKER_SERVER_ADDRESS` should be a combination of your DNS label and the location/region you placed your resource group in
