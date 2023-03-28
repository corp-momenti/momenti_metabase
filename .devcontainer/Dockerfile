ARG UBUNTU_VERSION=jammy-20230308
FROM ubuntu:${UBUNTU_VERSION}

# for devcontainer
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# for common script
ARG INSTALL_ZSH="false"
ARG UPGRADE_PACKAGES="true"
ARG COMMON_SCRIPT_SOURCE="https://raw.githubusercontent.com/microsoft/vscode-dev-containers/main/script-library/common-debian.sh"
ARG COMMON_SCRIPT_SHA="dev-mode"

# for docker script
ARG ENABLE_NONROOT_DOCKER="true"
ARG USE_MOBY="true"
ARG DOCKER_VERSION="latest"
ARG DOCKER_SCRIPT_SOURCE="https://raw.githubusercontent.com/microsoft/vscode-dev-containers/main/script-library/docker-in-docker-debian.sh"

# Enable new "BUILDKIT" mode for Docker CLI
ENV DOCKER_BUILDKIT=1

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive  
RUN apt-get -y install --no-install-recommends \
    curl \
    ca-certificates
RUN curl -sSL ${COMMON_SCRIPT_SOURCE} -o /tmp/common-setup.sh
RUN curl -sSL ${DOCKER_SCRIPT_SOURCE} -o /tmp/docker-setup.sh
RUN /bin/bash /tmp/common-setup.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}"
RUN /bin/bash /tmp/docker-setup.sh "${ENABLE_NONROOT_DOCKER}" "${USERNAME}" "{USER_MOBY}" "${DOCKER_VERSION}"
RUN apt-get clean -y && rm -rf /tmp/common-setup.sh && rm -rf /tmp/docker-setup.sh

VOLUME [ "/var/lib/docker" ]

ENTRYPOINT [ "/usr/local/share/docker-init.sh"]
CMD [ "sleep", "infinity"]