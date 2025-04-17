FROM ubuntu:22.04

# Non-interaktif agar tidak ada prompt saat install
ENV DEBIAN_FRONTEND=noninteractive

# Install paket dasar
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    software-properties-common \
    iptables \
    uidmap \
    git \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# Tambahkan Docker GPG key & repository
RUN mkdir -p /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
    https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
    tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker engine
RUN apt-get update && apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && \
    rm -rf /var/lib/apt/lists/*

# Tambahkan user default ke grup docker
RUN groupadd docker && usermod -aG docker root

# Set Docker daemon berjalan saat container dijalankan
CMD ["dockerd-entrypoint.sh"]
