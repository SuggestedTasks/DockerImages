# Instructions to build : https://krishansubudhi.github.io/development/2019/09/23/CreatingDockerImage.html
# Copied from https://hub.docker.com/r/krishansubudhi/transformers_pytorch
FROM mcr.microsoft.com/azureml/openmpi4.1.0-cuda11.0.3-cudnn8-ubuntu18.04

# # NCCL 2.4 does not work with PyTorch, uninstall
# RUN apt-get update && apt-get --purge remove libnccl2 -y --allow-change-held-packages

# # Install cuda
# RUN apt-get -y update && apt-get -y install --no-install-recommends libnccl2 libnccl-dev

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
    /opt/miniconda/envs/amlbert/bin/pip install --no-cache-dir pip install torch==1.8.1+cu111 torchvision==0.9.1+cu111 torchaudio==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html &&\
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
# SHA is something the user can touch to force recreation of this Docker layer,
# and therefore force cloning of the latest version of Apex
RUN SHA=2_3_2020 git clone https://github.com/NVIDIA/apex.git
RUN cd apex && \
/opt/miniconda/envs/amlbert/bin/pip install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" . && \
cd .. && \
rm -rf apex

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
