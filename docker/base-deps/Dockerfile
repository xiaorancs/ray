# The base-deps Docker image installs main libraries needed to run Ray

FROM ubuntu:focal
ENV TZ=America/Los_Angeles
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y && apt-get upgrade -y \
    && apt-get install -y \
        git \
        wget \
        cmake \
        build-essential \
        curl \
        unzip \
        tmux \
        screen \
        rsync \
        openssh-client \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && wget \
        --quiet "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh" \
        -O /tmp/miniconda.sh \
    && /bin/bash /tmp/miniconda.sh -b -u -p $HOME/anaconda3 \
    && $HOME/anaconda3/bin/conda init \ 
    && echo 'export PATH=$HOME/anaconda3/bin:$PATH' > /etc/profile.d/conda.sh \
    && rm /tmp/miniconda.sh \
    && $HOME/anaconda3/bin/conda install -y \
        libgcc python=3.7.7 \ 
    && $HOME/anaconda3/bin/conda clean -y --all \
    && $HOME/anaconda3/bin/pip install --no-cache-dir \
        flatbuffers \
        cython==0.29.0 \
        numpy==1.15.4 \
    # To avoid the following error on Jenkins:
    # AttributeError: 'numpy.ufunc' object has no attribute '__module__'
    && $HOME/anaconda3/bin/pip uninstall -y dask

# TODO(ilr) $HOME seems to point to result in "" instead of "/root"
ENV PATH "/root/anaconda3/bin:$PATH"
