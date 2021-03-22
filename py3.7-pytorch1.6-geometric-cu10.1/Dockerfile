FROM pytorch/pytorch:1.6.0-cuda10.1-cudnn7-devel
# FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04

# ENV PATH /opt/conda/bin:$PATH
ENV PATH /usr/local/cuda-10.1/bin:$PATH
ENV LD_LIBRARY_PATH /usr/lib/x86_64-linux-gnu:/usr/local/cuda-10.1/lib64:$LD_LIBRARY_PATH
ENV CUDA_HOME /usr/local/cuda-10.1
ENV CPATH /usr/local/cuda-10.1/include

RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade -i https://opentuna.cn/pypi/web/simple " && \
    CONDA_INSTALL="conda install -y" && \
    rm -rf /var/lib/apt/lists/* \
           /etc/apt/sources.list.d/cuda.list \
           /etc/apt/sources.list.d/nvidia-ml.list && \
    apt-get update && \
# ==================================================================
# tools
# ------------------------------------------------------------------
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        apt-utils \
        build-essential \
        ca-certificates \
        cmake \
        wget \
        git \
        vim \
        htop \
        tmux \
        openssh-client \
        openssh-server \
        libboost-dev \
        libboost-thread-dev \
        libboost-filesystem-dev \
        libglib2.0-0 \
        libsm6 \
        libxext6 \
        libxrender-dev \
        libgl1-mesa-glx \
        python3-opencv \
        && \
# ==================================================================
# conda
# ------------------------------------------------------------------
    # wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    # /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    # rm ~/miniconda.sh && \
    conda config --set show_channel_urls yes && \
    conda config --add channels conda-forge && \
    conda config --add channels pytorch && \
    $CONDA_INSTALL \
        python=3.7 && \
    $CONDA_INSTALL \
        # pytorch \
        # torchvision \
        # torchaudio \
        # cudatoolkit=10.1 \
        Cython \
        visdom \
        sk-video \
        imageio \
        h5py \
        tensorboard \
        tensorboardX \
        matplotlib \
        tqdm \
        scikit-learn \
        scipy \
        pillow \
        munkres \
        six \
        nibabel \
        easydict \
        pandas \
        yacs \
        wget \
        pytest \
        cffi \
        lmdb \
        gym \
        av \
        openh264 = 2.1.0 \
        && \
# ==================================================================
# pip
# ------------------------------------------------------------------
    pip install torch-scatter -f https://pytorch-geometric.com/whl/torch-1.6.0+cu101.html && \
    pip install torch-sparse -f https://pytorch-geometric.com/whl/torch-1.6.0+cu101.html && \
    pip install torch-cluster -f https://pytorch-geometric.com/whl/torch-1.6.0+cu101.html && \
    pip install torch-spline-conv -f https://pytorch-geometric.com/whl/torch-1.6.0+cu101.html && \
    pip install torch-geometric && \
    $PIP_INSTALL \
        opencv-python \
        opencv-contrib-python \
        cython-bbox \
        && \
    conda clean -y --all && \
# ==================================================================
# config & cleanup
# ------------------------------------------------------------------
    ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/* && \
    chmod -R 777 /root && \
    mkdir /.cache && \
    chmod -R 777 /.cache && \
    mkdir /.config && \
    chmod -R 777 /.config

ENV TMPDIR /tmp
ENV TEMP /tmp
ENV HOME /root

EXPOSE 6006