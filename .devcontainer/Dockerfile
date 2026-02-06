FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED=1

# System Dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3 \
    python3-venv \
    python3-pip \
    curl \
    jq \
    git \
    uuid-runtime \
    openssh-client \
    ca-certificates \
    docker.io \
 && rm -rf /var/lib/apt/lists/*

WORKDIR /workspace

# Default to bash shell (other shells available at /usr/bin/fish and /usr/bin/zsh)
ENV SHELL=/bin/bash \
    DOCKER_BUILDKIT=1
    
# Mount for docker-in-docker 
VOLUME [ "/var/lib/docker" ]    

# -------------------------
# Jupyter Base
# -------------------------
RUN python3 -m venv /opt/jupyter \
 && /opt/jupyter/bin/pip install --upgrade pip \
 && /opt/jupyter/bin/pip install jupyterlab ipykernel \
 && /opt/jupyter/bin/python -m ipykernel install \
      --sys-prefix --name=jupyter --display-name="Python (jupyter)"
      
# -------------------------
# kind
# -------------------------
RUN curl -Lo kind "https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64" \
    && chmod +x kind \
    && mv kind /usr/local/bin/

    
RUN curl -L https://github.com/mc-b/duk/archive/refs/heads/master.tar.gz | tar xz --strip-components=3 duk-master/data/jupyter --exclude='*/'

CMD [ "sleep", "infinity" ]

    