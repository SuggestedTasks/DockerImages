FROM mcr.microsoft.com/azureml/base-gpu:openmpi3.1.2-cuda10.1-cudnn7-ubuntu18.04
RUN apt-get update


# create conda environment
RUN conda update -n base -c defaults conda -y
RUN conda create -n titles python=3.8 -y
RUN echo ". /opt/miniconda/etc/profile.d/conda.sh" >> ~/.bashrc

#install torch latest
RUN conda install pytorch==1.11.0 torchvision==0.12.0 torchaudio==0.11.0 cudatoolkit=10.2 -c pytorch


# Cuda toolkit other than 1.2 makes GPUs invisible. Base image issue
# RUN conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch -c conda-forge
# RUN conda install pytorch torchvision torchaudio cudatoolkit=10.2 -c pytorch -y -n titles
RUN /opt/miniconda/envs/titles/bin/pip3 install --no-cache-dir torch torchvision torchaudio

COPY . /workdir_1
WORKDIR /workdir_1

# RUN /opt/miniconda/envs/titles/bin/pip3 install -U -e . 
# RUN /opt/miniconda/envs/titles/bin/pip3 install -U -r requirements.txt

RUN /opt/miniconda/envs/titles/bin/pip3 install transformers==4.25.1
RUN /opt/miniconda/envs/titles/bin/pip3 install datasets==2.2.2
RUN /opt/miniconda/envs/titles/bin/pip3 install pandas==1.3.5
RUN /opt/miniconda/envs/titles/bin/pip3 install rouge-score==0.0.4
RUN /opt/miniconda/envs/titles/bin/pip3 install nltk=3.5
RUN /opt/miniconda/envs/titles/bin/pip3 install tqdm
RUN /opt/miniconda/envs/titles/bin/pip3 install tensorboard
RUN /opt/miniconda/envs/titles/bin/pip3 install azureml-sdk
RUN /opt/miniconda/envs/titles/bin/pip3 install matplotlib
RUN /opt/miniconda/envs/titles/bin/pip3 install sklearn
RUN /opt/miniconda/envs/titles/bin/pip3 install scipy
RUN /opt/miniconda/envs/titles/bin/pip3 install colorama
RUN /opt/miniconda/envs/titles/bin/pip3 install keras
RUN /opt/miniconda/envs/titles/bin/pip3 install tensorflow tensorflow-gpu
RUN /opt/miniconda/envs/titles/bin/pip3 install contractions
RUN /opt/miniconda/envs/titles/bin/pip3 install SentencePiece
RUN /opt/miniconda/envs/titles/bin/pip3 install seaborn
RUN /opt/miniconda/envs/titles/bin/pip3 install pytorch_lightning
RUN /opt/miniconda/envs/titles/bin/pip3 install python-dotenv
RUN /opt/miniconda/envs/titles/bin/pip3 install jsonlines

# Download nltk resources
RUN python -m nltk.downloader punkt