FROM fedora:39

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    UV_SYSTEM_PYTHON=1 \
    PATH="/root/.local/bin:$PATH"

# Install system dependencies
RUN dnf update -y && \
    dnf install -y \
    python3.12 \
    python3.12-devel \
    python3-pip \
    git \
    curl \
    wget \
    gcc \
    gcc-c++ \
    make \
    openssl-devel \
    bzip2-devel \
    libffi-devel \
    zlib-devel \
    && dnf clean all

# Set Python 3.12 as default
RUN alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1 && \
    alternatives --install /usr/bin/python python /usr/bin/python3.12 1

# Install uv (modern Python package installer)
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

# Install ruff (Python linter and formatter)
RUN /root/.local/bin/uv tool install ruff

# Install Jupyter
RUN /root/.local/bin/uv tool install jupyter

# Create workspace directory
WORKDIR /workspace

# Expose Jupyter port
EXPOSE 8888

CMD ["/bin/bash"]