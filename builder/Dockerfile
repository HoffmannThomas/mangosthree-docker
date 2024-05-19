FROM gcc:12-bookworm as builder
ARG MANGOS_SERVER_VERSION=master
ARG THREAD_COUNT="-j8"

RUN apt-get update -qq && \
    apt-get install openssl libssl-dev cmake -y
RUN git clone https://github.com/mangosthree/server.git -b ${MANGOS_SERVER_VERSION} --recursive
RUN cd server && \
    cmake . -DBUILD_MANGOSD=1 -DBUILD_REALMD=1 -DBUILD_TOOLS=0 -DCONF_DIR=conf/ && \
    make ${THREAD_COUNT} && \
    make install ${THREAD_COUNT}