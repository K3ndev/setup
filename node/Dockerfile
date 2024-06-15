# Use the official Node.js image
FROM node:latest

# Install pnpm globally
RUN npm install -g pnpm

## git 
RUN apt install git
RUN git config --global user.name "K3ndev"
RUN git config --global user.email "racelisjk@gmail.com"

# docker build --tag custom-node .

# go to your target dir
# docker run -it -v .:/projects/<yourProjectName> custom-node sh

# recommended extension for vscode
# Dev Containers (ms-vscode-remote.remote-containers)