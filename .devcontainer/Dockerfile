FROM debian:sid

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update && \
    apt-get -y install git gnupg patch ssh

ARG USERNAME
RUN useradd "${USERNAME}" -ms '/bin/bash'

ARG COMPOSE_PROJECT_NAME
COPY --chmod=755 'dotfiles_hook' '/usr/local/bin'
RUN install -d -o "${USERNAME}" -g "${USERNAME}" "/home/${USERNAME}/dotfiles" && \
    install -d -o "${USERNAME}" -g "${USERNAME}" "/workspaces/${COMPOSE_PROJECT_NAME}" && \
    sed -i '/PS1.*\\\$/s/\\\$/\\n\0/' "/home/${USERNAME}/.bashrc"
