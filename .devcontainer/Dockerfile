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

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive  
RUN apt-get -y install --no-install-recommends curl ca-certificates 
RUN curl -sSL ${COMMON_SCRIPT_SOURCE} -o /tmp/common-setup.sh
RUN /bin/bash /tmp/common-setup.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}"
# RUN apt-get clean -y && rm -rf /tmp/common-setup.sh
# RUN bash -c "$(curl -fsSL "https://raw.githubusercontent.com/microsoft/vscode-dev-containers/main/script-library/common-debian.sh")" -- "${INSTALL_ZSH}" "vscode" "1000" "1000" "true"
# RUN apt-get clean -y && rm -rf /var/lib/apt/lists/*
USER ${USERNAME}
ENV PATH=/home/${USERNAME}/.local/bin:${PATH}
