# Dockerfile
ARG IMG_NAME
ARG IMG_TAG

FROM ${IMG_NAME}:${IMG_TAG}
MAINTAINER Mohamed Meabed <meabed@me.io>

ARG OPENSSL_VER
ARG OPENSSL_PREFIX

ENV DEBIAN_FRONTEND noninteractive
RUN export LANG=C.UTF-8 && export LC_ALL=en_US.UTF-8

ENV BUILD_PACKAGES \
    build-essential \
    pkg-config \
    libsslcommon2-dev \
    wget

RUN apt-get update &&  \
    apt-get -qq install -y ${BUILD_PACKAGES} && \
    cd /tmp && wget -q -O ${OPENSSL_VER}.tar.gz https://www.openssl.org/source/${OPENSSL_VER}.tar.gz && \
    tar xfz ${OPENSSL_VER}.tar.gz && \
    cd ${OPENSSL_VER} && \
    ./config shared --openssldir=${OPENSSL_PREFIX} && \
    make > /dev/null && \
    make test && \
    make install_sw > /dev/null && \
    ldconfig && \
    openssl version -a && \
    echo -e "\n\nSuccess: Installed ${OPENSSL_VER} in ${OPENSSL_PREFIX}\n" && \
    apt-get purge --auto-remove -y ${BUILD_PACKAGES} ;\
    apt-get autoremove --purge -y ;\
    apt-get clean -y ;\
    rm -rf /var/lib/apt/* ; \
    rm -rf /var/lib/dpkg/info/* ; \
    rm -rf /var/lib/cache/* ; \
    rm -rf /var/lib/log/* ; \
    rm -rf /var/tmp/* ; \
    rm -rf /tmp/*
