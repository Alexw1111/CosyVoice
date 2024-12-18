FROM dockerpull.org/nvidia/cuda:12.1.0-cudnn8-devel-ubuntu22.04

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV DEBIAN_FRONTEN=noninteractive
ENV PYTHONUNBUFFERED=1
SHELL ["/bin/bash", "--login", "-c"]

# 设置apt清华源
RUN sed -i 's/archive.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list && \
    sed -i 's/security.ubuntu.com/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list

# 安装系统依赖和Python
RUN apt-get update -y --fix-missing && \
    apt-get install -y \
    git \
    build-essential \
    curl \
    wget \
    ffmpeg \
    unzip \
    git-lfs \
    sox \
    libsox-dev \
    python3.10 \
    python3-pip && \
    apt-get clean && \
    git lfs install

# 设置pip清华源
RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple/ && \
    pip config set install.trusted-host pypi.tuna.tsinghua.edu.cn

WORKDIR /workspace

ENV PYTHONPATH="${PYTHONPATH}:/workspace/CosyVoice:/workspace/CosyVoice/third_party/Matcha-TTS"

# 克隆项目并安装依赖
RUN git clone --recursive https://kkgithub.com/FunAudioLLM/CosyVoice.git

# 安装项目依赖
RUN pip install pynini==2.1.5 && \
    cd CosyVoice && \
    pip install -r requirements.txt