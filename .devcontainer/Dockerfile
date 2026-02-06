FROM mcr.microsoft.com/devcontainers/universal:5-noble

RUN mkdir -p /workspace 
WORKDIR /workspace

# -------------------------
# kind
# -------------------------
RUN curl -Lo kind "https://kind.sigs.k8s.io/dl/latest/kind-linux-arm64" \
    && chmod +x kind \
    && mv kind /usr/local/bin/

    
RUN curl -L https://github.com/mc-b/duk/archive/refs/heads/master.tar.gz | tar xz --strip-components=3 duk-master/data/jupyter --exclude='*/'
    
