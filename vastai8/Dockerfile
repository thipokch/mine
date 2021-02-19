
FROM nvidia/cuda:8.0-devel-ubuntu16.04

WORKDIR /

# Package and dependency setup
RUN apt update \
    && apt install -y git \
    tmux \
    wget \
    nano 
    
RUN wget https://github.com/no-fee-ethereum-mining/nsfminer/releases/download/v1.2.2/nsfminer_1.2.2-ubuntu_16.04-cuda_10.2-opencl.tgz \
    && tar -xzvf nsfminer_1.2.2-ubuntu_16.04-cuda_10.2-opencl.tgz \
    && mv nsfminer /usr/local/bin/

RUN wget https://github.com/xmrig/xmrig/releases/download/v6.8.2/xmrig-6.8.2-focal-x64.tar.gz \
    && tar -xzvf xmrig-6.8.2-focal-x64.tar.gz \
    && cd xmrig-6.8.2 \
    && mv xmrig config.json /usr/local/bin/

# Env setup
ENV GPU_FORCE_64BIT_PTR=0
ENV GPU_MAX_HEAP_SIZE=100
ENV GPU_USE_SYNC_OBJECTS=1
ENV GPU_MAX_ALLOC_PERCENT=100
ENV GPU_SINGLE_ALLOC_PERCENT=100