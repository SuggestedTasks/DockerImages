FROM mcr.microsoft.com/azureml/base:openmpi3.1.2-ubuntu18.04
#FROM mcr.microsoft.com/azureml/base-gpu:openmpi3.1.2-cuda10.1-cudnn7-ubuntu18.04
RUN apt-get update


# create conda environment
RUN conda update -n base -c defaults conda -y
RUN conda create -n actionItems python=3.8 -y
RUN echo ". /opt/miniconda/etc/profile.d/conda.sh" >> ~/.bashrc

#install torch latest
# Cuda toolkit other than 1.2 makes GPUs invisible. Base image issue
RUN conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch -c conda-forge


COPY . /workdir_1
WORKDIR /workdir_1

# RUN /opt/miniconda/envs/actionItems/bin/pip install -U -e . 
# RUN /opt/miniconda/envs/actionItems/bin/pip install -U -r requirements.txt

# RUN /opt/miniconda/envs/actionItems/bin/pip install torchvision
RUN /opt/miniconda/envs/actionItems/bin/pip install transformers
RUN /opt/miniconda/envs/actionItems/bin/pip install pandas
RUN /opt/miniconda/envs/actionItems/bin/pip install tqdm
RUN /opt/miniconda/envs/actionItems/bin/pip install tensorboard
RUN /opt/miniconda/envs/actionItems/bin/pip install azureml-sdk
RUN /opt/miniconda/envs/actionItems/bin/pip install matplotlib
RUN /opt/miniconda/envs/actionItems/bin/pip install sklearn
RUN /opt/miniconda/envs/actionItems/bin/pip install scipy
RUN /opt/miniconda/envs/actionItems/bin/pip install colorama
RUN /opt/miniconda/envs/actionItems/bin/pip install keras
RUN /opt/miniconda/envs/actionItems/bin/pip install tensorflow tensorflow-gpu
RUN /opt/miniconda/envs/actionItems/bin/pip install contractions
RUN /opt/miniconda/envs/actionItems/bin/pip install nltk
RUN /opt/miniconda/envs/actionItems/bin/pip install SentencePiece
RUN /opt/miniconda/envs/actionItems/bin/pip install seaborn


# Install apex
RUN mkdir -p /tmp && \
    cd /tmp
# SHA is something the user can touch to force recreation of this Docker layer,
# and therefore force cloning of the latest version of Apex
RUN git clone https://github.com/NVIDIA/apex.git
RUN cd apex && \
    /opt/miniconda/envs/actionItems/bin/pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./ && \
    cd .. && \
    rm -rf apex
    
    
# Instructions to update docker image. (replace krishansubudhi with your dockerhub account name)
# https://krishansubudhi.github.io/development/2019/09/23/CreatingDockerImage.html

# In a VM, Build
# docker build --rm -t krishansubudhi/marlin:latest .

# Test
# docker run --gpus all -it -d -p 5000:5000 krishansubudhi/marlin:latest
# docker attach <guid from the above command>

# Push new image to dockerhub
# docker push krishansubudhi/marlin:latest