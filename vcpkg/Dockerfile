FROM alpine:3.16.2

# update and get the necessary tools
RUN apk update && \
    apk add build-base pkgconfig zip unzip curl git tar wget make linux-headers g++ openssl-dev libressl-dev python3-dev && \
    cd /usr/bin && ln python3 python

# build cmake since we need version 3.24.1
RUN wget https://github.com/Kitware/CMake/releases/download/v3.24.1/cmake-3.24.1.tar.gz && \
    tar -xvf cmake-3.24.1.tar.gz && \
    cd cmake-3.24.1 && \
    ./bootstrap && \
    make -j4 && \
    make install

# build and install ninja since we need version 1.10
RUN git clone https://github.com/ninja-build/ninja.git && \
    cd ninja && \
    ./configure.py --bootstrap && \
    cmake -Bbuild-cmake && \
    cmake --build build-cmake && \
    cp ./ninja /usr/bin

# build and install vcpkg
RUN git clone https://github.com/Microsoft/vcpkg.git && \
    cd ./vcpkg && \
    ./bootstrap-vcpkg.sh -disableMetrics

