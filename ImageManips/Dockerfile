FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
    git \
    wget \
    cmake \
    libglew-dev \
    libegl1-mesa-dev \
    qtdeclarative5-dev \
    ffmpeg \
    libopencv-dev \
    libboost-filesystem-dev \   
    libboost-system-dev \
    lsb-release 


RUN apt-get update && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
    && apt-get update && apt-get install -y gcc-6 g++-6

RUN git clone https://github.com/GPUOpen-Tools/Compressonator.git

WORKDIR /Compressonator/Compressonator/Applications/CompressonatorCLI/Make/
RUN wget http://download.savannah.nongnu.org/releases/openexr/ilmbase-2.2.0.tar.gz  && \
    wget http://download.savannah.nongnu.org/releases/openexr/openexr-2.2.0.tar.gz 

RUN tar xvfz openexr-2.2.0.tar.gz && tar xvfz ilmbase-2.2.0.tar.gz

WORKDIR /Compressonator/Compressonator/Applications/CompressonatorCLI/Make/ilmbase-2.2.0
RUN export CC=/usr/bin/gcc-6 && export CXX=/usr/bin/g++-6 \
    && cmake -DCMAKE_INSTALL_PREFIX=/usr/local/ilmbase22build/ . \
    && make -j 4 \
    && make install

WORKDIR /Compressonator/Compressonator/Applications/CompressonatorCLI/Make/openexr-2.2.0
RUN export CC=/usr/bin/gcc-6 && export CXX=/usr/bin/g++-6 \
    && cmake -DILMBASE_PACKAGE_PREFIX=/usr/local/ilmbase22build/ -DCMAKE_INSTALL_PREFIX=/usr/local/openexr22build/ . \
    && make -j 4 \
    &&  make install

#compile dds
WORKDIR /Compressonator/Compressonator/Applications/_Plugins/CImage/DDS/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

#compile astc
WORKDIR /Compressonator/Compressonator/Applications/_Plugins/CImage/ASTC/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

#compile EXR
WORKDIR /Compressonator/Compressonator/Applications/_Plugins/CImage/EXR/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

#compile TGA
WORKDIR /Compressonator/Compressonator/Applications/_Plugins/CImage/TGA/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

#compile KTX
WORKDIR /Compressonator/Compressonator/Applications/_Plugins/CImage/KTX/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

#compile CFilter
WORKDIR /Compressonator/Compressonator/Applications/_Plugins/CFilter/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

# #compile CAnalysis
WORKDIR /Compressonator/Compressonator/Applications/_Plugins/CAnalysis/Analysis/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

#compile main Make file
WORKDIR /Compressonator/Compressonator/Make/
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make

#compile CLI Make file
WORKDIR /Compressonator/Compressonator/Applications/CompressonatorCLI/Make
RUN export CC=/usr/bin/gcc-6 && \
    export CXX=/usr/bin/g++-6 && \
    rm -f CMakeCache.txt && \
    rm -f -r CMakeFiles && \
    rm -f cmake_install.cmake && \
    rm -f Makefile && \
    cmake -G Unix\ Makefiles && \
    make