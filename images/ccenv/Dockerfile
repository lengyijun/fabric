# Copyright IBM Corp. All Rights Reserved.
#
# SPDX-License-Identifier: Apache-2.0

FROM ubuntu:bionic

RUN apt-get update \
 && apt-get install -y \
    wget \
    curl \
    git \
    build-essential \
    ca-certificates \
    protobuf-compiler \
    python-protobuf \
    libprotobuf-dev \
    libssl-dev \
    libcurl4-openssl-dev \
    libtool \
    cmake \
    vim \
    g++ \
    gcc \
    make \
 && apt-get -y -q upgrade \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

COPY go1.14.1.linux-amd64.tar.gz /tmp
RUN tar -C /usr/local -xzf  /tmp/go1.14.1.linux-amd64.tar.gz && rm /tmp/go1.14.1.linux-amd64.tar.gz 

ENV GOPATH=/go
ENV PATH=$PATH:/usr/local/go/bin:/go/bin

ARG SGX_REPO=https://download.01.org/intel-sgx/linux-2.6/ubuntu18.04-server
ARG SGX_LIB_COMMON=libsgx-enclave-common_2.6.100.51363-bionic1_amd64.deb
ARG SGX_SDK_BIN=sgx_linux_x64_sdk_2.6.100.51363.bin

# Create a place for our SGX SDK
RUN mkdir -p /opt/intel \
 && mkdir -p /etc/init

WORKDIR /opt/intel

# Install SGX COMMON
RUN wget ${SGX_REPO}/${SGX_LIB_COMMON} \
 && dpkg -i ${SGX_LIB_COMMON}

# Install SGX SDK
RUN wget ${SGX_REPO}/${SGX_SDK_BIN} \
 && chmod +x ${SGX_SDK_BIN} \
 && echo "yes" | ./${SGX_SDK_BIN} \
 && rm ${SGX_SDK_BIN}

ENV SGX_SDK=/opt/intel/sgxsdk
ENV PATH=$PATH:$SGX_SDK/bin:$SGX_SDK/bin/x64
ENV PKG_CONFIG_PATH=$PKG_CONFIG_PATH:$SGX_SDK/pkgconfig
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$SGX_SDK/sdk_libs

RUN mkdir -p /chaincode/output /chaincode/input
RUN addgroup --gid 500 chaincode && adduser --uid 500 --disabled-password  --home /home/chaincode --ingroup chaincode --gecos '' chaincode
RUN chown -R chaincode:chaincode /chaincode
USER chaincode
