FROM alpine:3.18.4

# update and get the necessary tools
RUN apk update && \
    apk add build-base pkgconfig zip unzip curl git tar wget make linux-headers g++ libressl-dev python3-dev

# build cmake since we need version 3.27.6
RUN wget https://github.com/Kitware/CMake/releases/download/v3.27.6/cmake-3.27.6.tar.gz && \
    tar -xvf cmake-3.27.6.tar.gz && \
    cd cmake-3.27.6 && \
    ./bootstrap && \
    make -j4 && \
    make install

# build and install ninja since we need version 1.11
RUN git clone https://github.com/ninja-build/ninja.git && \
    cd ninja && \
    ./configure.py --bootstrap && \
    cmake -Bbuild-cmake && \
    cmake --build build-cmake && \
    cp ./ninja /usr/bin

ENV VCPKG_FORCE_SYSTEM_BINARIES=1

# build and install vcpkg
RUN git clone https://github.com/Microsoft/vcpkg.git &&\
    cd ./vcpkg && \
    ./bootstrap-vcpkg.sh

