FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

# Install dependencies
WORKDIR /install
COPY ./apt-list.txt .
RUN apt-get update && \
    cat apt-list.txt | \
    sed 's/#.*$//g' | \
    sed '/^$/d' | \
    tr '\n' ' ' | \
    xargs apt-get install -y

# NPM Dev dependencies
COPY ./package.json .
RUN npm install && npm install -g --only=dev
ENV NODE_PATH=/install/node_modules

# Clean up
RUN apt-get autoremove -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/*

CMD [ "/bin/sh" ]