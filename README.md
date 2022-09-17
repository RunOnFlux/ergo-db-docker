# ergo-db-docker
This repo's purpose is to build the latest image for the Ergo-DB component. It is designed to be compatible with FluxOS.

The Dockerfile builds Postgres 14 with Ergo Platform's [Explorer-Backend DB Schema](https://github.com/ergoplatform/explorer-backend/blob/master/modules/explorer-core/src/main/resources/db/V9__Schema.sql).

Install [Docker](https://docs.docker.com/engine/install/) and follow the below instructions to build the image and push it to Docker-Hub.

```
# In the Dockerfile, update the version if required
# Latest stable version can be found at Ergo Platform's [Explorer-Backend](https://github.com/ergoplatform/explorer-backend/releases)
ARG EXPLORER_VERSION=9.16.6

# In the Dockerfile, make sure that the link is valid
# If Ergo Platform have updated the schema version or changed the file path,
# please use the latest raw github URL
ARG SCHEMA=https://raw.githubusercontent.com/ergoplatform/explorer-backend/$EXPLORER_VERSION/modules/explorer-core/src/main/resources/db/V9__Schema.sql

# Build the image and tag it as "ergo-db"
docker build . -t ergo-db

# Log in to Docker-Hub with your username and password
docker login -u your-username

# Tag the image with the Docker-Hub repo tag
docker tag ergo-db runonflux/ergo-db:latest

# Push the image to Docker-Hub (each layer may take a few mins to push)
docker push runonflux/ergo-db:latest

# Use the image in FluxOS or in your Docker-Compose file
runonflux/ergo-db:latest
```
