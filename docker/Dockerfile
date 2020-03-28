
FROM ubuntu:18.04

ARG TAG

ENV PYTHON_VERSION 3.8.0
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN \
    sed -i 's@# deb-src http://archive.ubuntu.com/ubuntu/ bionic main restricted@deb-src http://archive.ubuntu.com/ubuntu/ bionic main restricted@' /etc/apt/sources.list \
    && apt-get update && apt-get -y upgrade \
    && apt-get -y install \
    ca-certificates \
    openssl \
    libssl1.1 \
    && dpkg-query -Wf '${Package}\n' | sort > init_pkgs \
    && apt-get -y install \
    wget \
    && apt-get -y build-dep python3.6 \
    && dpkg-query -Wf '${Package}\n' | sort > new_pkgs \
    && wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz \
    && tar xf Python-$PYTHON_VERSION.tgz \
    && cd Python-$PYTHON_VERSION \
    && sed -i 's/$(MAKE) run_profile_task//' Makefile.pre.in \
    && ./configure --enable-optimizations --with-ensurepip=install \
    && make \
    && make install \
    && cd .. \
    && rm -rf Python-$PYTHON_VERSION \
    && rm Python-$PYTHON_VERSION.tgz \
    && ln -sf /usr/local/bin/python3 /usr/bin/python \
    && ln -s /usr/local/bin/pip3 /usr/bin/pip \
    && pip install --upgrade pip \
    && apt-get -y purge $(diff -u init_pkgs new_pkgs | grep -E "^\+" | cut -d + -f2- | sed -n '1!p') \
    && apt-get clean \
    && rm init_pkgs new_pkgs \
    && rm -rf \
    /root/.cache/pip \
    && find / -type d -name __pycache__ -exec rm -r {} \+

WORKDIR /usr/src

RUN apt-get install gcc -y
RUN apt-get -y install python3.8* python3-dev python-dev

ENV PYTHON_CONFIGURE_OPTS "--enable-shared"

RUN pip install pyinstaller