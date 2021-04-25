FROM mcr.microsoft.com/azureml/base:openmpi3.1.2-ubuntu18.04
RUN apt-get update


# create conda environment
RUN conda update -n base -c defaults conda -y
RUN conda create -n actionItems python=3.8 -y
RUN echo ". /opt/miniconda/etc/profile.d/conda.sh" >> ~/.bashrc

#install torch latest
# Cuda toolkit other than 1.2 makes GPUs invisible. Base image issue
RUN conda install pytorch cudatoolkit=10.2 -c pytorch -y -n actionItems


COPY . /workdir_1
WORKDIR /workdir_1

# RUN /opt/miniconda/envs/actionItems/bin/pip install -U -e . 
# RUN /opt/miniconda/envs/actionItems/bin/pip install -U -r requirements.txt

RUN /opt/miniconda/envs/actionItems/bin/pip install torchvision
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



# Instructions to update docker image. (replace krishansubudhi with your dockerhub account name)
# https://krishansubudhi.github.io/development/2019/09/23/CreatingDockerImage.html

# In a VM, Build
# docker build --rm -t krishansubudhi/marlin:latest .

# Test
# docker run --gpus all -it -d -p 5000:5000 krishansubudhi/marlin:latest
# docker attach <guid from the above command>

# Push new image to dockerhub
# docker push krishansubudhi/marlin:latest