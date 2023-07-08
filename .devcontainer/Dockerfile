FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive


RUN apt-get -y update --no-install-recommends \
    && apt-get -y install --no-install-recommends \
    build-essential \
    curl \
    ca-certificates \
    apt-utils \
    dialog \
    git \
    vim \
    && apt-get autoremove -y \
    && apt-get clean -y

RUN apt -y install linux-tools-generic hwdata
RUN update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/*-generic/usbip 20

RUN cd ~/  && \
    git clone https://github.com/leramirez55/ambpro2_sdk.git

RUN cd ~/ambpro2_sdk/tools && \
    cat asdk-10.3.0-linux-newlib-build-3633-x86_64.tar.bz2.* | tar jxvf -
    

RUN chmod +x ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE/mp/elf2bin.linux && \
    chmod +x ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE/mp/checksum.linux

RUN apt-get -y install cmake 
RUN cd ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE && \
    mkdir build && \
    cd build && \
    export PATH=$PATH:~/ambpro2_sdk/tools/asdk-10.3.0/linux/newlib/bin && \
    cmake .. -G"Unix Makefiles" -DCMAKE_TOOLCHAIN_FILE=../toolchain.cmake -DVIDEO_EXAMPLE=ON && \
    cmake --build . --target flash_nn -j4

