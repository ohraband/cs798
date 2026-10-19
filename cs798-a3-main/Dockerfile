# Start with a stock Ubuntu 24.04 image
FROM ubuntu:24.04

# Install basic packages
# Added 'time' package for bench-experiment's CPU time measurement
RUN apt update && apt install -y build-essential cmake python3-pip libssl-dev git time

# Install openfhe
RUN git clone https://github.com/openfheorg/openfhe-development openfhe && \
    cd openfhe && git checkout v1.4.0 && \
    cmake -B build -DBUILD_EXAMPLES=ON -DBUILD_EXTRAS=ON -DBUILD_SHARED=ON . && \
    make -C build -j`nproc` && make -C build install && cd .. && \
    rm -rf openfhe

RUN ldconfig

# Install our openfhe-python fork that contains bindings for some
# functions that are missing from the upstream release
RUN apt update && apt install -y python3-pybind11
RUN git clone https://git-crysp.uwaterloo.ca/iang/openfhe-python-fork openfhe-python && \
    cd openfhe-python && git checkout 978cbef8d803e4eb9ee149b263dd52a274040f52 && \
    cmake -B build -DCMAKE_INSTALL_PREFIX=/usr/lib/python3/dist-packages/ . && \
    make -C build -j`nproc` && make -C build install && \
    cd .. && rm -rf openfhe-python

# Do not edit anything above this line.

# Copy your code directory into the image under /root
COPY code /root/code/

# Make /root/code the default working directory
WORKDIR /root/code

# For C++: build the binary with make, which should create the binary a3
# and ensure it's in the current directory.
# NOTE: If your binary is C++/C, you must uncomment and run these commands!
# Assuming C++ based on the environment setup.
# RUN cmake .
# RUN make

# For Python: just make the a3 python script executable, in case it
# wasn't marked as such in the git repo
RUN chmod 755 a3

# Make the bench-experiment script executable
RUN chmod 755 bench-experiment