FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install -y git \
                       wget \
                       curl \
                       jq \
                       python-pip \
                       lsb-release \
                       apt-transport-https \
                       software-properties-common \
                       apt-utils \
                       vim \
                       groff-base \
                       unzip && \

    # Create work directories
    mkdir /root/bin && \
    mkdir /root/tmp && \
    mkdir /root/work && \

    # Setup .bashrc for user's directory
    echo "" >> /root/.bashrc && \
    echo '# users private bin directories' >> /root/.bashrc && \
    echo 'export PATH=$PATH:/root/bin' >> /root/.bashrc && \

    # Install Ansible
    pip2 install ansible && \

    # Install AWS CLI
    pip2 install awscli && \

    # Install AliCloud ROS CLI
    pip2 install aliyun-ros-cli && \

    # Setup Terraform 
    cd /root/bin && \
    wget https://releases.hashicorp.com/terraform/0.11.10/terraform_0.11.10_linux_amd64.zip && \
    unzip terraform_0.11.10_linux_amd64.zip && \
    rm -f terraform_0.11.10_linux_amd64.zip && \

    # Setup Packer
    cd /root/bin && \
    wget https://releases.hashicorp.com/packer/1.3.2/packer_1.3.2_linux_amd64.zip && \
    unzip packer_1.3.2_linux_amd64.zip && \
    rm -f packer_1.3.2_linux_amd64.zip && \

    # Setup Alibaba cloud plugin for Packer
    mkdir -p /root/.packer.d/plugins && \
    cd /root/.packer.d/plugins && \
    wget https://github.com/alibaba/packer-provider/releases/download/V1.3.0/packer-builder-alicloud-ecs_linux-amd64.tgz && \
    tar zxf packer-builder-alicloud-ecs_linux-amd64.tgz && \

    # Setup Alibaba Cloud CLI
    wget http://aliyun-cli.oss-cn-hangzhou.aliyuncs.com/aliyun-cli-linux-3.0.2-amd64.tgz && \
    tar xzf aliyun-cli-linux-3.0.2-amd64.tgz && \
    rm -f aliyun-cli-linux-3.0.2-amd64.tgz && \

    # Install Google Cloud CLI
    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update -y && \
    apt-get install google-cloud-sdk -y && \

    # Install Azure CLI
    AZ_REPO=$(lsb_release -cs) && \
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | tee /etc/apt/sources.list.d/azure-cli.list && \
    apt-key --keyring /etc/apt/trusted.gpg.d/Microsoft.gpg adv \
            --keyserver packages.microsoft.com \
            --recv-keys BC528686B50D79E339D3721CEB3E94ADBE1229CF && \
    apt-get update && \
    apt-get install azure-cli && \

    # Install kubectl command
    curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list && \
    apt-get update && \
    apt-get install -y kubectl

# Create volume for work directory
VOLUME /root/work
