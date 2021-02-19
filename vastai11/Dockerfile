
FROM nvidia/cuda:11.0.3-devel-ubuntu20.04

WORKDIR /

ENV TZ="America/New_York"

# Package and dependency setup
RUN ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime \
    && apt update \
    && apt install -y git \
    cmake \
    mesa-common-dev \
    libdbus-1-dev \
    tmux \
    wget \
    nano
    
# Git repo set up
RUN git clone https://github.com/no-fee-ethereum-mining/nsfminer.git; \
    cd nsfminer; \
    ls; \
    git checkout tags/v1.3.2 -b ; \
    git submodule update --init --recursive

# Build
RUN pwd; \
    cd nsfminer; \
    pwd; \
    ls; \
    mkdir build; \
    cd build; \
    pwd; \
    cmake .. -DETHASHCUDA=ON -DETHASHCL=OFF -DETHSTRATUM=ON; \
    cmake --build .; \
    make install

RUN wget https://github.com/xmrig/xmrig/releases/download/v6.8.2/xmrig-6.8.2-focal-x64.tar.gz \
    && tar -xzvf xmrig-6.8.2-focal-x64.tar.gz \
    && cd xmrig-6.8.2 \
    && cp xmrig config.json /usr/local/bin/

# Env setup
ENV GPU_FORCE_64BIT_PTR=0
ENV GPU_MAX_HEAP_SIZE=100
ENV GPU_USE_SYNC_OBJECTS=1
ENV GPU_MAX_ALLOC_PERCENT=100
ENV GPU_SINGLE_ALLOC_PERCENT=100
