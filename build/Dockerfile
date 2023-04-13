FROM ubuntu:latest

RUN apt update \ 
    && apt install -y \
    build-essential software-properties-common

RUN apt install -y \
    git curl sudo bash wget htop neofetch nano vim locales

RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

RUN useradd coder --create-home --shell=/bin/bash --uid=1000 --user-group && \
    echo "coder ALL=(ALL) NOPASSWD:ALL" >>/etc/sudoers.d/nopasswd         && \
    echo "permit nopass coder as root" >> /etc/doas.conf

USER 1000
WORKDIR /home/coder

# Uses "Spaceship" theme with some customization. Uses some bundled plugins and installs some more from github
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.5/zsh-in-docker.sh)" -- \
    -t https://github.com/denysdovhan/spaceship-prompt \
    -a 'SPACESHIP_PROMPT_ADD_NEWLINE="false"' \
    -a 'SPACESHIP_PROMPT_SEPARATE_LINE="false"' \
    -p git \
    -p ssh-agent \
    -p npm \
    -p https://github.com/zsh-users/zsh-autosuggestions \
    -p https://github.com/zsh-users/zsh-completions


RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
RUN export NVM_DIR="$HOME/.nvm" && \
    [ -s "$NVM_DIR/nvm.sh" ]    && \
    . "$NVM_DIR/nvm.sh"         && \
    nvm install node            && \
    npm i -g pnpm npm


ENV LANG="en_US.UTF-8"
