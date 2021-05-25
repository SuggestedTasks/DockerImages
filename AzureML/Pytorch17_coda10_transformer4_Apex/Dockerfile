# Instructions to build : https://krishansubudhi.github.io/development/2019/09/23/CreatingDockerImage.html
# Copied from https://hub.docker.com/r/krishansubudhi/transformers_pytorch
FROM mcr.microsoft.com/azureml/base-gpu:openmpi3.1.2-cuda10.0-cudnn7-ubuntu16.04

# NCCL 2.4 does not work with PyTorch, uninstall
RUN apt-get update && apt-get --purge remove libnccl2 -y --allow-change-held-packages

# Install cuda
RUN apt-get -y update && apt-get -y install --no-install-recommends libnccl2=2.3.7-1+cuda10.0 libnccl-dev=2.3.7-1+cuda10.0

# Creating a conda env called amlbert
RUN [ "/bin/bash", "-c", "conda create -n amlbert Python=3.7 && source activate amlbert && conda install pip"]

# Within the env, install pytorch 1.3, transformers, and moew
RUN ldconfig /usr/local/cuda/lib64/stubs && \
    # Install GPUtil
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir GPUtil && \
    # Install AzureML SDK
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir azureml-defaults && \
    # Install PyTorch
    #/opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir https://download.pytorch.org/whl/cu100/torch-1.0.1-cp36-cp36m-linux_x86_64.whl &&\
    #/opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir https://download.pytorch.org/whl/cu100/torch-1.3.0%2Bcu100-cp36-cp36m-linux_x86_64.whl &&\ 
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir torch==1.7.1+cu101 torchvision==0.8.2+cu101 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html &&\
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir mkl && \
    ldconfig

#RUN /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir pytorch-pretrained-bert==0.6.2 && \
RUN /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir tensorboardX

RUN /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir transformers==4.3.3

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    wget \
    vim \
    tmux \
    unzip \
    htop

# Install apex
RUN mkdir -p /tmp && \
    cd /tmp
# SHA is something the user can touch to force recreation of this Docker layer,
# and therefore force cloning of the latest version of Apex
WORKDIR /tmp/unique_for_apex
# uninstall Apex if present, twice to make absolutely sure :)
RUN pip uninstall -y apex || :
RUN pip uninstall -y apex || :
# SHA is something the user can touch to force recreation of this Docker layer,
# and therefore force cloning of the latest version of Apex
RUN SHA=ToUcHMe git clone https://github.com/NVIDIA/apex.git
RUN pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" .
WORKDIR /workspace

RUN /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir scipy && \
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir sklearn && \
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir matplotlib && \
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir seaborn && \
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir nltk && \
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir tensorboard && \
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir sentencepiece && \
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir msgpack &&\
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir psutil &&\
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir rouge


RUN /opt/miniconda/envs/amlbert/bin/python -c "import nltk; nltk.download('punkt')"
RUN /opt/miniconda/envs/amlbert/bin/pip install -I https://matrixdeploystorageeus.blob.core.windows.net/matrixlib/matrixlib-0.1.2018481.tar.gz