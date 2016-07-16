FROM ubuntu:trusty

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    libssl-dev \
    libreadline-dev \
    python \
    zip \
    zlib1g-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
 
#Test
RUN mkdir /opt/fh

RUN locale-gen en_US.UTF-8 \
 && /usr/sbin/update-locale LANG=en_US.UTF-8 \
 && dpkg-reconfigure -f noninteractive locales

RUN git clone https://github.com/rbenv/rbenv.git $HOME/.rbenv \
 && cd $HOME/.rbenv \
 && src/configure \
 && make -C src \
 && ln -s $HOME/.rbenv/bin/rbenv /usr/local/bin

RUN eval "$(rbenv init -)" \
 && git clone https://github.com/rbenv/ruby-build.git $(rbenv root)/plugins/ruby-build

RUN eval "$(rbenv init -)" \
 && git clone https://github.com/sstephenson/rbenv-default-gems.git $(rbenv root)/plugins/rbenv-default-gems \
 && echo 'bundler' >> $(rbenv root)/default-gems

RUN eval "$(rbenv init -)" \
 && rbenv install 1.9.3-p551

RUN eval "$(rbenv init -)" \
&& rbenv install 2.2.5

RUN eval "$(rbenv init -)" \
&& rbenv install 2.3.1

RUN \
    apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ubuntu-toolchain-r/test && apt-get update && \
    apt-get upgrade -y && \
    apt-get dist-upgrade -y && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
