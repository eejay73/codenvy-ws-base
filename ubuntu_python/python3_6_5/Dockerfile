FROM eclipse/stack-base:ubuntu
RUN sudo apt-get purge -y python.* &&   sudo apt-get update &&   sudo apt-get install -y --no-install-recommends \
    autoconf \
    automake \
    bzip2 \
    file \
    g++ \
    gcc \
    imagemagick \
    libbz2-dev \
    libc6-dev \
    libcurl4-openssl-dev libdb-dev libevent-dev libffi-dev libgdbm-dev libgeoip-dev libglib2.0-dev libjpeg-dev \
    libkrb5-dev liblzma-dev libmagickcore-dev libmagickwand-dev libmysqlclient-dev libncurses-dev libpng-dev \
    libpq-dev libreadline-dev libsqlite3-dev libssl-dev libtool libwebp-dev libxml2-dev libxslt-dev libyaml-dev make patch xz-utils zlib1g-dev
ENV LANG=C.UTF-8
ENV PYTHON_VERSION=3.6.5
ENV PYTHON_PIP_VERSION=10.0.0
RUN set -ex && sudo curl -fSL "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" -o python.tar.xz && sudo curl -fSL "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz.asc" -o python.tar.xz.asc && export GNUPGHOME="$(mktemp -d)" && sudo rm -r "$GNUPGHOME" python.tar.xz.asc && sudo mkdir -p /usr/src/python && sudo tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz && sudo rm python.tar.xz && cd /usr/src/python && sudo ./configure --enable-shared --enable-unicode=ucs4 && sudo make -j$(nproc) && sudo make install && sudo ldconfig && sudo pip3 install --upgrade --ignore-installed pip==$PYTHON_PIP_VERSION && sudo find /usr/local \( -type d -a -name test -o -name tests \) -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) -exec rm -rf '{}' + && sudo rm -rf /usr/src/python
RUN cd /usr/local/bin && sudo ln -s easy_install-3.6 easy_install && sudo ln -s idle3 idle && sudo ln -s pydoc3 pydoc && sudo ln -s python3 python && sudo ln -s python-config3 python-config
RUN sudo pip install --no-cache-dir virtualenv
EXPOSE 8080