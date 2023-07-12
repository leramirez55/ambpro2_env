FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

ENV PATH="/root/ambpro2_sdk/tools/asdk-10.3.0/linux/newlib/bin:/root/ambpro2_sdk/tools/Pro2_PG_tool _v1.3.0:${PATH}" 

RUN apt-get -y update --no-install-recommends && \
    apt-get -y install --no-install-recommends \
    build-essential \
    cmake \
    curl \
    ca-certificates \
    apt-utils \
    dialog \
    git \
    unzip \
    vim

RUN apt-get autoremove -y && \
    apt-get clean -y

RUN apt -y install linux-tools-generic hwdata
RUN update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/*-generic/usbip 20

RUN cd ~/  && \
    git clone https://github.com/leramirez55/ambpro2_sdk.git

RUN cd ~/ambpro2_sdk/tools && \
    cat asdk-10.3.0-linux-newlib-build-3633-x86_64.tar.bz2.* | tar jxvf -
    
#Fix Permission Problems in SDK
RUN chmod +x ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE/mp/elf2bin.linux && \
    chmod +x ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE/mp/checksum.linux

RUN mkdir ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE/build


RUN cd ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE/build && \
    cmake .. -G "Unix Makefiles" -DCMAKE_TOOLCHAIN_FILE=../toolchain.cmake -DVIDEO_EXAMPLE=ON

RUN cd ~/ambpro2_sdk/project/realtek_amebapro2_v0_example/GCC-RELEASE/build && \
    cmake --build . --target flash_nn -j4


RUN cd ~/ambpro2_sdk/tools && \
    unzip 'Pro2_PG_tool _v1.3.0.zip' && \
    cd 'Pro2_PG_tool _v1.3.0' && \
    chmod +x uartfwburn.linux
