
FROM nvidia/cuda:10.2-devel-ubuntu18.04

WORKDIR /

# Package and dependency setup
RUN apt update \
    && apt install -y git \
    tmux \
    wget \
    nano 
    
RUN wget https://github.com/no-fee-ethereum-mining/nsfminer/releases/download/v1.2.1/nsfminer-ubuntu-18.04-cuda-10.tgz \
    && tar -xzvf nsfminer-ubuntu-18.04-cuda-10.tgz \
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