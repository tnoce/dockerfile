FROM ubuntu:16.04
MAINTAINER sashiyama <yoshiki.sashiyama@nijibox.co.jp>
ENV ETH_ROOT /eth_data
RUN apt-get update && apt-get install -y git
RUN git clone -b release/1.3.6 https://github.com/ethereum/go-ethereum.git
RUN apt-get install -y build-essential libgmp3-dev golang
RUN make -C go-ethereum geth
RUN cp go-ethereum/build/bin/geth /usr/bin/
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:ethereum/ethereum
RUN apt-get update && apt-get install -y solc
EXPOSE 8545
RUN mkdir $ETH_ROOT
WORKDIR $ETH_ROOT
ENTRYPOINT /bin/bash
