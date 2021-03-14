# ==================================================================
# module list
# ------------------------------------------------------------------
# python        3.7    (conda)
# pytorch       1.0.1  (conda)
# tensorboardx  1.6    (conda)
# ffpmeg        4.1    (conda)
# ==================================================================
FROM pytorch/pytorch:1.6.0-cuda10.1-cudnn7-runtime

ENV PATH /opt/conda/bin:$PATH
ENV PATH /usr/local/cuda-10.1/bin:$PATH
ENV LD_LIBRARY_PATH /usr/lib/x86_64-linux-gnu:/usr/local/cuda-10.1/lib64:$LD_LIBRARY_PATH

RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade " && \
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
        && \
# ==================================================================
# conda
# ------------------------------------------------------------------
    conda config --set show_channel_urls yes && \
    conda config --add channels conda-forge && \
    $CONDA_INSTALL \
        python=3.7 && \
    $CONDA_INSTALL \
        ipython \
        Cython \
        ffmpeg \
        visdom \
        sk-video \
        imageio \
        h5py \
        tensorboard \
        cffi \
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
        lmdb \
        opencv-python \
        opencv-contrib-python \
        Pillow \
        six \
        scipy \
        munkres \
        nibabel \
        pandas \
        matplotlib \
        tqdm \
        scikit-learn \
        pytest \
        wget \
        gym \
        && \
    conda clean -y --all && \
# ==================================================================
# config & cleanup
# ------------------------------------------------------------------
    ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*
EXPOSE 6006