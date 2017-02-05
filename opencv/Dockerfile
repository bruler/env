FROM ubuntu:16.04
MAINTAINER Kapil Gupta <kpgupta98@gmail.com>

RUN	apt-get update
RUN	apt-get install -y -q wget curl
RUN	apt-get install -y -q build-essential
RUN	apt-get install -y -q cmake

RUN apt-get install -y -q build-essential cmake git pkg-config

RUN apt-get install -y -q libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev
RUN apt-get install -y -q libgtk2.0-dev
RUN apt-get install -y -q libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
RUN apt-get install -y -q libatlas-base-dev gfortran
RUN apt-get install -y -q libhdf5-dev

RUN apt-get install -y -q python-pip
RUN pip install --upgrade pip
RUN apt-get install -y -q python2.7 python2.7-dev
RUN pip install numpy

RUN pip install virtualenv virtualenvwrapper
RUN rm -rf ~/.cache/pip

RUN apt-get autoclean && apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN \
  cd ~ && \
  git clone https://github.com/Itseez/opencv.git && \
  cd opencv && \
  pwd && \
  git checkout 3.1.0 && \

  cd ~ && \
  git clone https://github.com/Itseez/opencv_contrib.git && \
  cd opencv_contrib && \
  git checkout 3.1.0 && \

   cd /root/opencv && \
   mkdir build && \
   cd build && \
   cmake -D CMAKE_BUILD_TYPE=RELEASE \
     -D CMAKE_INSTALL_PREFIX=/usr/local \
     -D INSTALL_C_EXAMPLES=OFF \
     -D INSTALL_PYTHON_EXAMPLES=ON \
     -D OPENCV_EXTRA_MODULES_PATH=/root/opencv_contrib/modules \
     -D BUILD_EXAMPLES=ON .. && \


   cd ~/opencv/build && \
   make -j $(nproc) && \
   make install && \
   ldconfig && \

   cp ~/opencv/build/lib/cv2.so /usr/local/lib/python2.7/dist-packages/
