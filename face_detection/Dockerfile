# This is a sample Dockerfile you can modify to deploy your own app based on face_recognition on the GPU
# In order to run Docker in the GPU you will need to install Nvidia-Docker: https://github.com/NVIDIA/nvidia-docker

FROM nvidia/cuda:10.2-cudnn7-devel

# Install face recognition dependencies

RUN apt update -y; apt install -y \
git \
cmake \
libsm6 \
libxext6 \
libxrender-dev \
python3 \
python3-pip

RUN pip3 install scikit-build

# Install compilers

RUN apt install -y software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt update -y; apt install -y gcc-6 g++-6

RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-6 50
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-6 50

#Install dlib 

RUN git clone -b 'v19.19' --single-branch https://github.com/davisking/dlib.git
RUN mkdir -p /dlib/build

RUN cmake -H/dlib -B/dlib/build -DDLIB_USE_CUDA=1 -DUSE_AVX_INSTRUCTIONS=1
RUN cmake --build /dlib/build

RUN cd /dlib; python3 /dlib/setup.py install

RUN pip3 install click numpy

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8 
