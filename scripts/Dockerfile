# build apron-node
FROM paritytech/ci-linux:production as builder

LABEL maintainer="apron-dev"
ARG RUST_VERSION=nightly-2020-10-06
ARG PROFILE=debug
ARG GIT_REPO="https://github.com/apron-network/apron-node.git"
ARG GIT_BRANCH="master"

RUN git clone --recursive ${GIT_REPO}
WORKDIR /builds/apron-node
RUN rustup default stable
RUN rustup uninstall nightly
RUN rustup toolchain install ${RUST_VERSION}
RUN rustup target add wasm32-unknown-unknown --toolchain ${RUST_VERSION}

RUN cargo build
RUN cp target/${PROFILE}/apron-node /apron-node

# build apron frontend
FROM paritytech/ci-linux:production as frontend_builder

ARG FRONT_REPO="https://github.com/polkadot-js/apps.git"
ARG FRONT_BRANCH="v0.71.2"

RUN git clone -b ${FRONT_BRANCH} ${FRONT_REPO}
WORKDIR /builds/apps
RUN apt update && apt install gnupg2 curl ca-certificates -y
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt update && apt install yarn -y
RUN YARN_CHECKSUM_BEHAVIOR=update yarn && yarn build:www

# build gateway
FROM golang:1.16.0-buster AS build-env
ARG GATEWAY_REPO="https://github.com/Apron-Network/apron_gateway.git"
ARG GATEWAY_BRANCH="master"

RUN git clone ${GATEWAY_REPO}
WORKDIR /go/apron_gateway
RUN make build

FROM ubuntu
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install curl ca-certificates npm nodejs -y
RUN npm install -g serve
COPY --from=builder /apron-node /

COPY --from=frontend_builder /builds/apps/packages/apps /apps

COPY --from=build-env /go/apron_gateway/gw /app/gw

ENV PATH /opt/conda3/bin:$PATH
ENV REDIS_SERVER=localhost:6379
ENV PROXY_PORT=8080
ENV ADMIN_ADDR=127.0.0.1:8082

EXPOSE 30333 9933 9944 8000 3001

