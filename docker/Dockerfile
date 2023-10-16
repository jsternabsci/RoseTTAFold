FROM nvidia/cuda:11.2.2-runtime-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN \
    # Update package list
    apt-get update -y && \
    # Install...
    apt-get install -y \
    git \
    vim \
    wget \
    python3 \
    python3-dev \
    python3-pip \
    tmux \
    # Remove package lists
    && rm -rf /var/lib/apt/lists/*

# Install conda
RUN cd /home && \
    wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.10.3-Linux-x86_64.sh && \
    bash Miniconda3-py38_4.10.3-Linux-x86_64.sh -b -p $HOME/miniconda
RUN $HOME/miniconda/bin/conda init bash

RUN git clone https://github.com/RosettaCommons/RoseTTAFold.git

WORKDIR /RoseTTAFold

# Install conda dependencies
RUN $HOME/miniconda/bin/conda env create -f RoseTTAFold-linux.yml

RUN echo "export PATH=$HOME/miniconda/bin:$PATH" >> $HOME/.bashrc
RUN echo "conda init bash" >> $HOME/.bashrc
# RUN echo "conda activate RoseTTAFold" >> $HOME/.bashrc

# Donwload model weights
RUN wget https://files.ipd.uw.edu/pub/RoseTTAFold/weights.tar.gz
RUN tar xfz weights.tar.gz

RUN ./install_dependencies.sh

ENTRYPOINT ["/bin/bash"]