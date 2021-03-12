FROM ubuntu:20.04
USER root
ARG DEBIAN_FRONTEND=noninteractive
ENV AL_FOLIO_BASE_REPO="https://github.com/alshedivat/al-folio"
ENV LC_ALL="C.UTF-8"
ENV LANG="en_US.UTF-8"
ENV LANGUAGE="en_US.UTF-8"

RUN echo 'export LC_ALL="C.UTF-8"' >> ~/.bashrc && \
  echo 'export LANG="en_US.UTF-8"' >> ~/.bashrc && \
  echo 'export LANGUAGE="en_US.UTF-8"' >> ~/.bashrc

RUN apt-get update && apt-get install --fix-missing -y --no-install-recommends \
  bash \
  bash-completion \
  build-essential \
  ca-certificates \
  curl \
  git \
  grep \
  nano \
  python3-pip \
  ruby-full \
  unzip \
  vim \
  wget \
  zip \
  zlib1g-dev

RUN echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc && \
  echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc && \
  echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc && \
  export PATH="$HOME/gems/bin:$PATH"

RUN gem install jekyll bundler

RUN cd ~/ && git clone $AL_FOLIO_BASE_REPO && \
  cd al-folio && \
  bundle install
