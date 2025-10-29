FROM mcr.microsoft.com/devcontainers/python:3.11
RUN apt-get update && apt-get install -y curl git wget unzip build-essential && rm -rf /var/lib/apt/lists/*
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && apt-get install -y nodejs
RUN npm install -g yarn
WORKDIR /workspace
RUN pip install --upgrade pip && pip install mkdocs mkdocs-material mkdocs-mermaid2
USER codespace