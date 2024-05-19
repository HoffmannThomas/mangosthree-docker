FROM gcc:7.3.0 as mangosthree/builder
ARG MANGOS_SERVER_VERSION=master
ARG THREAD_COUNT="-j4"

RUN apt-get update -qq && \
    apt-get install openssl libssl-dev cmake -y && \
    git clone https://github.com/mangosthree/server.git -b ${MANGOS_SERVER_VERSION} --recursive && \
    cd server && \
    cmake . -DBUILD_MANGOSD=No -DBUILD_TOOLS=No -DCONF_DIR=conf/ && \
    make ${THREAD_COUNT} && \
    make install ${THREAD_COUNT}