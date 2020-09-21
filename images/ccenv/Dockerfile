# Copyright IBM Corp. All Rights Reserved.
#
# SPDX-License-Identifier: Apache-2.0

FROM baiduxlab/sgx-rust:latest

ENV PKG_CONFIG_PATH=$PKG_CONFIG_PATH:$SGX_SDK/pkgconfig
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$SGX_SDK/sdk_libs

ADD go1.15.2.linux-amd64.tar.gz /usr/local
ENV GOPATH=/go
ENV GOROOT=/usr/local/go
ENV PATH=$PATH:/usr/local/go/bin:/go/bin:/root/.cargo/bin

RUN mkdir -p /chaincode/output /chaincode/input
RUN git clone https://github.com/apache/incubator-teaclave-sgx-sdk /opt/incubator-teaclave-sgx-sdk --depth=1
RUN ln -s /opt/sgxsdk /opt/intel/sgxsdk
