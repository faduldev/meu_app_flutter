FROM mcr.microsoft.com/devcontainers/base:ubuntu

USER root

ENV DEBIAN_FRONTEND=noninteractive
ENV FLUTTER_HOME=/opt/flutter
ENV PATH=/opt/flutter/bin:/opt/flutter/bin/cache/dart-sdk/bin:${PATH}

# Dependências básicas para Flutter
RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
    xz-utils \
    zip \
    libglu1-mesa \
    ca-certificates \
    wget \
    gnupg \
    && rm -rf /var/lib/apt/lists/*

# Instala o Google Chrome
RUN wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get update \
    && apt-get install -y ./google-chrome-stable_current_amd64.deb \
    && rm google-chrome-stable_current_amd64.deb \
    && rm -rf /var/lib/apt/lists/*

# Baixa o Flutter Stable diretamente do repositório oficial
RUN git clone --depth 1 --branch stable \
    https://github.com/flutter/flutter.git \
    ${FLUTTER_HOME}

# Permite que o usuário vscode utilize o Flutter
RUN chown -R vscode:vscode ${FLUTTER_HOME}

# Pré-baixa componentes necessários do Flutter
USER vscode

RUN flutter --version \
    && flutter config --enable-web

USER root

# Volta para o usuário normal do Dev Container
USER vscode