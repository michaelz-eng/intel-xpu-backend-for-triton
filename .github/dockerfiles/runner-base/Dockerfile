FROM summerwind/actions-runner:ubuntu-22.04

USER root

RUN set -ex; \
    export DEBIAN_FRONTEND=noninteractive; \
    echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/intel-graphics.gpg] https://repositories.intel.com/gpu/ubuntu jammy unified' > /etc/apt/sources.list.d/intel-gpu-jammy.list; \
    curl -sSL https://repositories.intel.com/gpu/intel-graphics.key | gpg --dearmor --output /usr/share/keyrings/intel-graphics.gpg; \
    echo "deb [arch=amd64 signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" > /etc/apt/sources.list.d/github-cli.list;\
    curl -sSL https://cli.github.com/packages/githubcli-archive-keyring.gpg > /usr/share/keyrings/githubcli-archive-keyring.gpg; \
    apt-get update -y; \
    apt-get install -y --no-install-recommends --fix-missing \
      intel-opencl-icd \
      clinfo \
      intel-level-zero-gpu \
      level-zero \
      level-zero-dev libigc-dev intel-igc-cm libigdfcl-dev libigfxcmrt-dev \
      \
      build-essential \
      zlib1g-dev \
      cmake \
      ninja-build \
      ncurses-term \
      pkg-config \
      \
      libpng-dev libjpeg-dev libsndfile1-dev libxml2-dev libxslt1-dev \
      libgl1-mesa-glx  \
      fontconfig libfontconfig1-dev \
      libpango-1.0-0 libpangoft2-1.0-0 \
      libsdl2-dev libsdl2-2.0-0 \
      \
      gh \
    ; \
    rm -rf /var/lib/apt/lists/*

USER runner
WORKDIR $HOME

SHELL ["/bin/bash", "-xec"]

# TODO: install only necessary components
RUN \
  curl -sSLO https://registrationcenter-download.intel.com/akdlm/IRC_NAS/52723419-d344-42bf-93ca-867606409cf0/l_intel-for-pytorch-gpu-dev_p_0.5.0.49_offline.sh; \
  sh l_intel-for-pytorch-gpu*.sh -a --silent --eula accept; \
  rm l_intel-for-pytorch-gpu*.sh

RUN \
  curl -sSLO https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh; \
  sh Miniconda3-latest-Linux-x86_64.sh -b; \
  rm Miniconda3-latest-Linux-x86_64.sh
