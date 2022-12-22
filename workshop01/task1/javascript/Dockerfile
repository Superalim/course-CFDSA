# base image
ARG NODE_VER=18

FROM node:${NODE_VER}

ARG PORT=3000
ARG INSTANCE_NAME
ARG INSTANCE_HASH

# Building the Image
# Create /app and cd into it
WORKDIR /app

# Copy app into /app
ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD public public
ADD views views

# Install the dependencies
RUN npm ci

# Install curl
RUN apt update && apt install curl -y

# Running the Image
# Set any environment variables required by the application

VOLUME /external

# curl has to be installed into the base image
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl http://localhost:${PORT}/healthz || exit 1

EXPOSE ${PORT}

ENTRYPOINT [ "node", "main.js" ]