FROM debian:bullseye-slim

# Install temporary packages which are required to install other software
USER root
SHELL [ "/bin/bash", "-o", "pipefail", "-c" ]
RUN \
  export DEBIAN_FRONTEND=noninteractive && \
  apt-get update && \
  apt-get install --yes --no-install-recommends \
    curl=7.74.0-1.3+deb11u7 \
    ca-certificates=20210119 \
    && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*
RUN echo "Install additional software here"
# Remove temporary packages
RUN \
  export DEBIAN_FRONTEND=noninteractive && \
  apt-get purge --yes \
    curl \
    && \
  apt-get --yes autoremove

# Create and switch to non-privileged user
RUN \
  groupadd --gid 1000 user && \
  useradd --uid 1000 --gid user --shell /bin/bash --create-home user
USER user

ENTRYPOINT [ "/bin/bash" ]
