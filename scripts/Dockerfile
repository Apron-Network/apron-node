# build apron-node
FROM paritytech/ci-linux:production as builder

ARG GIT_REPO="https://github.com/Apron-Network/apron-node.git"
ARG GIT_BRANCH="upgrade_contract"

RUN git clone -b ${GIT_BRANCH} --recursive ${GIT_REPO}
WORKDIR /builds/apron-node

RUN rustup default nightly-2021-11-08 && rustup target add wasm32-unknown-unknown
RUN cargo build --release
RUN cp target/release/apron-node /apron-node

# build polkadot and apron  frontend
FROM ubuntu:18.04 as frontend_builder

ARG FRONT_REPO="https://github.com/polkadot-js/apps.git"
ARG FRONT_BRANCH="master"

RUN apt-get update && apt-get install --no-install-recommends -y git gnupg curl ca-certificates

# install nodejs
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install --no-install-recommends -y nodejs && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*
RUN npm install yarn -g

RUN mkdir /builds && cd /builds && git clone -b ${FRONT_BRANCH} ${FRONT_REPO}
WORKDIR /builds/apps

RUN YARN_CHECKSUM_BEHAVIOR=update yarn && yarn build:www

FROM ubuntu
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install curl ca-certificates npm nodejs -y
RUN npm install -g serve
COPY --from=builder /apron-node /

COPY --from=frontend_builder /builds/apps/packages/apps /apps

EXPOSE 30333 9933 9944 8080 8082 2145

