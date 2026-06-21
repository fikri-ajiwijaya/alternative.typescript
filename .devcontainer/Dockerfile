FROM debian:sid

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update && \
    apt-get -y dist-upgrade && \
    apt-get -y autopurge

RUN apt-get -y install curl git gnupg jq less man parallel patch ssh vim wget xz-utils

RUN apt-get -y install libatomic1

ARG USERNAME
RUN useradd "${USERNAME}" -ms '/bin/bash'

RUN install -d -o "${USERNAME}" -g "${USERNAME}" '/workspaces/node_modules'

USER "${USERNAME}"

RUN curl -L 'https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh' | NODE_VERSION='node' bash && \
    NVM_DIR="${HOME}/.nvm" && \
    . "${NVM_DIR}/nvm.sh" && \
    npm install --no-save --prefix '/workspaces' '@types/node' 'esbuild' 'typescript'

USER root

ARG COMPOSE_PROJECT_NAME
COPY --chmod=644 --chown="${USERNAME}:${USERNAME}" '.vimrc' "/home/${USERNAME}"
COPY --chmod=755 'dotfiles_hook' '/usr/local/bin'
COPY --chmod=755 'template_hook' '/usr/local/bin'
RUN install -d -o "${USERNAME}" -g "${USERNAME}" "/home/${USERNAME}/dotfiles" && \
    install -d -o "${USERNAME}" -g "${USERNAME}" "/workspaces/${COMPOSE_PROJECT_NAME}" && \
    install -d -o "${USERNAME}" -g "${USERNAME}" "/workspaces/alternative/${COMPOSE_PROJECT_NAME}" && \
    sed -i '/PS1.*\\\$/s/\\\$/\\n\0/' "/home/${USERNAME}/.bashrc"
