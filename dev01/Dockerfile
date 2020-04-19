FROM centos:7

# epel
RUN yum -y install epel-release

# system update
RUN yum -y update && \
    yum install -y git \
                    jq \
                    wget \
                    curl \
                    unzip \
                    nmap \
                    python-pip \
                    vim

# ユーザーの作業ディレクトリを作成する
RUN mkdir /root/bin && \
    mkdir /root/tmp && \
    mkdir /root/work

# Setup .bashrc for user's directory
RUN echo "" >> /root/.bashrc && \
    echo '# users private bin directories' >> /root/.bashrc && \
    echo 'export PATH=$PATH:/root/bin' >> /root/.bashrc

# Setup Alibaba Cloud CLI
RUN wget http://aliyun-cli.oss-cn-hangzhou.aliyuncs.com/aliyun-cli-linux-3.0.2-amd64.tgz && \
    tar xzf aliyun-cli-linux-3.0.2-amd64.tgz && \
    rm -f aliyun-cli-linux-3.0.2-amd64.tgz && \
    cd / && \
    cp aliyun ~/bin/aliyun 

RUN pip2 install awscli

# Create volume for work directory
VOLUME /root/work