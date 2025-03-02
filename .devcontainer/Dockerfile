FROM mcr.microsoft.com/devcontainers/rust:1-1-bookworm

# Install system dependencies
RUN <<EOF
apt-get update && export DEBIAN_FRONTEND=noninteractive
apt-get -y install --no-install-recommends \
    build-essential \
    cmake \
    pkg-config \
    libssl-dev \
    clang \
    llvm \
    libudev-dev \
    libclang-dev \
    lld \
    git \
    curl \
    wget \
    python3 \
    python3-pip \
    jq
apt-get clean -y
rm -rf /var/lib/apt/lists/*
EOF

# Install Foundry
RUN <<EOF
curl -L https://foundry.paradigm.xyz | bash
/root/.foundry/bin/foundryup
EOF

# Install Rust components
RUN rustup component add llvm-tools rustc-dev

# Install sp1up
RUN <<EOF
curl -L https://sp1up.succinct.xyz | bash
/root/.sp1/bin/sp1up
EOF

# Install additional Rust tools
RUN cargo install cargo-watch cargo-nextest cargo-expand cargo-edit

# Set environment variables
ENV PATH="/root/.foundry/bin:/root/.sp1/bin:${PATH}"
ENV RUSTFLAGS="-C target-cpu=native"
