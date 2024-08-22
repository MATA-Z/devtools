FROM ubuntu:latest
SHELL ["/bin/bash", "-c"]

RUN apt-get update && \
    apt-get install -y \ 
    curl git wget zsh \ 
    build-essential pkg-config python3 python3-venv\
    && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash && \
    export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")" && \
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    && nvm install 20.17.0 \
    && nvm install 18.20.4 \
    && nvm install 16.20.2 \
    && nvm install 14.21.0 \
    && nvm install 12.22.1 \
    && nvm install 10.24.0 \
    && nvm use 20.17.0 \
    && npm install -g nrm yarn \
    && nrm use taobao \
    && rm -rf /var/lib/apt/lists/*
SHELL ["/bin/zsh", "-c"]
RUN git clone --depth=1 https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && sed -i '/^ZSH_THEME=.*/c ZSH_THEME="ys"' ~/.zshrc \
    && chsh -s /bin/zsh \
    && source ~/.zshrc 
# 安装 code-server 和扩展
ARG CODE_VERSION=4.10.1
RUN cd /usr/local/ && \
    wget https://github.com/coder/code-server/releases/download/v${CODE_VERSION}/code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    tar xf code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    ln -s  /usr/local/code-server-${CODE_VERSION}-linux-amd64/bin/code-server /usr/bin/code && \
    rm code-server-${CODE_VERSION}-linux-amd64.tar.gz && \
    wget https://open-vsx.org/api/MS-CEINTL/vscode-language-pack-zh-hans/1.75.0/file/MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix && \
    code --install-extension MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix && \
    rm MS-CEINTL.vscode-language-pack-zh-hans-1.75.0.vsix

EXPOSE 8080/tcp
CMD ["code", "--auth", "none", "--bind-addr", "0.0.0.0:8080"]