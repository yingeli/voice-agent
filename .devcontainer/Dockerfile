FROM nvcr.io/nvidia/tensorrt-llm/devel:1.1.0rc1

# Install baseline packages
RUN apt-get update && \
    apt-get install --yes --no-install-recommends --no-install-suggests \
    bash \
    build-essential \
    # containerd.io \
    curl \
    # docker-ce \
    # docker-ce-cli \
    # docker-buildx-plugin \
    # docker-compose-plugin \
    htop \
    jq \
    locales \
    man \
    pipx \
    # python3 \
    # python3-pip \
    # software-properties-common \
    sudo \
    # systemd \
    # systemd-sysv \
    unzip \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Enables Docker starting with systemd
# RUN systemctl enable docker

# Create a symlink for standalone docker-compose usage
# RUN ln -s /usr/libexec/docker/cli-plugins/docker-compose /usr/bin/docker-compose

# Generate the desired locale (en_US.UTF-8)
RUN locale-gen en_US.UTF-8

# Make typing unicode characters in the terminal work.
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

# Remove the `ubuntu` user and add a user `coder` so that you're not developing as the `root` user
RUN userdel -r ubuntu && \
    useradd coder \
    --create-home \
    --shell=/bin/bash \
    #--groups=docker \
    --uid=1000 \
    --user-group && \
    echo "coder ALL=(ALL) NOPASSWD:ALL" >>/etc/sudoers.d/nopasswd

USER coder
RUN pipx ensurepath # adds user's bin directory to PATH

# install rust
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y