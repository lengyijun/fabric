# Copyright IBM Corp. All Rights Reserved.
#
# SPDX-License-Identifier: Apache-2.0

FROM baiduxlab/sgx-rust:latest


RUN cd /opt \
 && git clone https://github.com/apache/incubator-teaclave-sgx-sdk --depth=1

# Create a place for our SGX SDK
RUN mkdir -p /opt/intel \
 && mkdir -p /etc/init \
 && ln -s /opt/sgxsdk /opt/intel/sgxsdk

WORKDIR /usr/local/bin

ENV SGX_SDK=/opt/sgxsdk
ENV PATH=$PATH:$SGX_SDK/bin:$SGX_SDK/bin/x64
ENV PKG_CONFIG_PATH=$PKG_CONFIG_PATH:$SGX_SDK/pkgconfig
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$SGX_SDK/sdk_libs

