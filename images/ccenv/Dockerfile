# Copyright IBM Corp. All Rights Reserved.
#
# SPDX-License-Identifier: Apache-2.0

FROM baiduxlab/sgx-rust:latest

RUN cd /opt \
 && git clone https://github.com/apache/incubator-teaclave-sgx-sdk --depth=1

# ARG SGX_REPO=https://download.01.org/intel-sgx/linux-2.6/ubuntu18.04-server
# ARG SGX_LIB_COMMON=libsgx-enclave-common_2.6.100.51363-bionic1_amd64.deb
# ARG SGX_SDK_BIN=sgx_linux_x64_sdk_2.6.100.51363.bin

# Create a place for our SGX SDK
RUN mkdir -p /opt/intel \
 && mkdir -p /etc/init  \
 && mkdir -p /chaincode/output /chaincode/input \
 && ln -s /opt/sgxsdk /opt/intel/sgxsdk

WORKDIR /opt/intel

ENV SGX_SDK=/opt/sgxsdk
ENV PATH=$PATH:$SGX_SDK/bin:$SGX_SDK/bin/x64
ENV PKG_CONFIG_PATH=$PKG_CONFIG_PATH:$SGX_SDK/pkgconfig
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$SGX_SDK/sdk_libs

ADD go1.14.4.linux-amd64.tar.gz /usr/local
ENV GOPATH=/go
ENV GOROOT=/usr/local/go
ENV PATH=$PATH:/usr/local/go/bin:/go/bin:/root/.cargo/bin


