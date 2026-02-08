FROM nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install -y wget curl ca-certificates git \
    gcc-10 g++-10 \
    git \
    cmake \
    ninja-build \
    build-essential \
    libboost-program-options-dev \
    libboost-graph-dev \
    libboost-system-dev \
    libeigen3-dev \
    libfreeimage-dev \
    libmetis-dev \
    libgoogle-glog-dev \
    libgtest-dev \
    libgmock-dev \
    libsqlite3-dev \
    libglew-dev \
    qt6-base-dev \
    libqt6opengl6-dev \
    libqt6openglwidgets6 \
    libcgal-dev \
    libceres-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libmkl-full-dev \
    ffmpeg

# Install Miniconda
ENV CONDA_DIR=/opt/conda
ENV PATH=$CONDA_DIR/bin:$PATH
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    /bin/bash /tmp/miniconda.sh -b -p $CONDA_DIR && \
    rm /tmp/miniconda.sh

# Build colmap
WORKDIR /tmp
ENV CC=gcc-10
ENV CXX=g++-10 
ENV CUDAHOSTCXX=/usr/bin/g++-10
RUN git clone https://github.com/colmap/colmap.git && \
    cd colmap && \
    git checkout 3.13.0 && \
    mkdir build && \
    cd build && \
    cmake .. -GNinja -DBLA_VENDOR=Intel10_64lp -DCMAKE_CUDA_ARCHITECTURES="89" && \
    ninja && \
    ninja install
