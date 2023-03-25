#FROM docker.io/ubuntu:22.04
FROM jupyter/docker-stacks-foundation

USER root
#install nodejs
RUN sudo apt-get update && \
    sudo apt-get install -y curl &&\
    curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
    sudo apt-get install -y nodejs

#install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - &&\
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list &&\
    sudo apt update && sudo apt install yarn

#install git
RUN sudo apt-get install git -y

#install jupyterlite
RUN git clone https://github.com/jupyterlite/jupyterlite && \
    cd jupyterlite && \
    python -m pip install -r requirements-docs.txt -r requirements-lint.txt

# install rtc package
RUN mamba install -c conda-forge jupyterlab-webrtc-docprovider

#test tool
RUN apt install vim -y && \
    npm install -g wscat

#EXPOSE 8000
WORKDIR /home/jovyan/jupyterlite
CMD ["doit","serve:docs:app"]