FROM ubuntu:latest

ARG USER=vscode
ARG HOME=/home/${USER}
ARG UID=1000
ARG GID=${UID}
ARG USER_GROUPS=audio,video

RUN apt-get update \
    && apt-get -y install \
        git \
        python3-dev python3-pip python3-setuptools python3-venv \
    #
    # Create a non-root user to use
    && groupadd -g ${GID} ${USER} \
    && useradd -u ${UID} -g ${GID} -m ${USER} -s $(which bash) \
    && if [ "${USER_GROUPS}" != "" ]; then usermod -a -G ${USER_GROUPS} ${USER}; fi \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

USER ${USER}

RUN mkdir -p ${HOME}/.vscode-server \
    && mkdir -p ${HOME}/workspace

SHELL ["/bin/bash", "-c"]
