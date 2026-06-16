FROM debian:sid

ARG USERNAME
RUN useradd "${USERNAME}" -ms '/bin/bash'

ARG COMPOSE_PROJECT_NAME
RUN install -d -o "${USERNAME}" -g "${USERNAME}" "/workspaces/${COMPOSE_PROJECT_NAME}"
