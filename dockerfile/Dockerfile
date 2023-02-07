FROM ubuntu:22.04

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get install -y \
    build-essential \
    cmake \
    libopencv-dev \
    libx11-dev \
    libfreetype6-dev \
    libxrandr-dev \
    libxinerama-dev \
    libxcursor-dev \
    libmagic-dev \
    libpoppler-cpp-dev \
    nano \
    git

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libtclap-dev

RUN mkdir -p /root/src \
    && cd /root/src \
    && git clone https://github.com/AlexeyAB/darknet.git \
    && cd darknet \
    && sed -i 's/LIBSO=0/LIBSO=1/g' Makefile \
    && make -j64 \
    && cp libdarknet.so /usr/local/lib/ \
    && cp include/darknet.h /usr/local/include/ \
    && ldconfig \
    && cd /root/src \
    && git clone https://github.com/stephanecharette/DarkHelp.git \
    && cd DarkHelp \
    && mkdir -p build \
    && cd build \
    && cmake -DCMAKE_BUILD_TYPE=Release .. \
    && make -j64 \
    && make package \
    && dpkg -i darkhelp*.deb \
    && cd /root/src && git clone https://github.com/stephanecharette/DarkMark.git \
    && mkdir -p /root/src/DarkMark/build \
    && cd /root/src/DarkMark/build \
    && cmake -DCMAKE_BUILD_TYPE=Release .. \
    && make -j64 \
    && make package \
    && dpkg -i darkmark*.deb

