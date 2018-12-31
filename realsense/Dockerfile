# This is an auto generated Dockerfile for ros:desktop-full
# generated from docker_images/create_ros_image.Dockerfile.em
FROM ubuntu:16.04.05

ENV DEBIAN_FRONTEND noninteractive

# nvidia-docker hooks
LABEL com.nvidia.volumes.needed="nvidia_driver"
ENV PATH /usr/local/nvidia/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64:${LD_LIBRARY_PATH}

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

RUN apt-get update && apt-get install -q -y tzdata && rm -rf /var/lib/apt/lists/*

# install ros packages
RUN apt-get update && apt-get install -y \
  cmake git vim pkg-config \
  sudo unzip ffmpeg qtbase5-dev \
  python-dev python3-dev python-numpy python3-numpy \
  libopencv-dev libgtk-3-dev libdc1394-22 libdc1394-22-dev libjpeg-dev libtiff5-dev \
  libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev \
  libv4l-dev libtbb-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev \
  libvorbis-dev libxvidcore-dev v4l-utils vtk6 \
  liblapacke-dev libopenblas-dev libgdal-dev checkinstall \
  libglfw3-dev libusb-1.0-0-dev

RUN wget https://github.com/opencv/opencv/archive/3.4.4.tar.gz
RUN tar xzf 3.4.3.tar.gz
RUN cd opencv-3.4.3 && mkdir build && cd build && \
cmake -G "Unix Makefiles" --build . -D BUILD_CUDA_STUBS=OFF -D BUILD_DOCS=OFF \
-D BUILD_EXAMPLES=OFF -D BUILD_JASPER=OFF -D BUILD_JPEG=OFF -D BUILD_OPENEXR=OFF \
-D BUILD_PACKAGE=ON -D BUILD_PERF_TESTS=OFF -D BUILD_PNG=OFF -D BUILD_SHARED_LIBS=ON \
-D BUILD_TBB=OFF -D BUILD_TESTS=OFF -D BUILD_TIFF=OFF -D BUILD_WITH_DEBUG_INFO=ON \
-D BUILD_ZLIB=OFF -D BUILD_WEBP=OFF -D BUILD_opencv_apps=ON -D BUILD_opencv_calib3d=ON \
-D BUILD_opencv_core=ON -D BUILD_opencv_cudaarithm=OFF -D BUILD_opencv_cudabgsegm=OFF \
-D BUILD_opencv_cudacodec=OFF -D BUILD_opencv_cudafeatures2d=OFF -D BUILD_opencv_cudafilters=OFF \
-D BUILD_opencv_cudaimgproc=OFF -D BUILD_opencv_cudalegacy=OFF -D BUILD_opencv_cudaobjdetect=OFF \
-D BUILD_opencv_cudaoptflow=OFF -D BUILD_opencv_cudastereo=OFF -D BUILD_opencv_cudawarping=OFF \
-D BUILD_opencv_cudev=OFF -D BUILD_opencv_features2d=ON -D BUILD_opencv_flann=ON \
-D BUILD_opencv_highgui=ON -D BUILD_opencv_imgcodecs=ON -D BUILD_opencv_imgproc=ON \
-D BUILD_opencv_java=OFF -D BUILD_opencv_ml=ON -D BUILD_opencv_objdetect=ON \
-D BUILD_opencv_photo=ON -D BUILD_opencv_python2=OFF -D BUILD_opencv_python3=ON \
-D BUILD_opencv_shape=ON -D BUILD_opencv_stitching=ON -D BUILD_opencv_superres=ON \
-D BUILD_opencv_ts=ON -D BUILD_opencv_video=ON -D BUILD_opencv_videoio=ON \
-D BUILD_opencv_videostab=ON -D BUILD_opencv_viz=OFF -D BUILD_opencv_world=OFF \
-D CMAKE_BUILD_TYPE=RELEASE -D WITH_1394=ON -D WITH_CUBLAS=OFF -D WITH_CUDA=OFF \
-D WITH_CUFFT=OFF -D WITH_EIGEN=ON -D WITH_FFMPEG=ON -D WITH_GDAL=OFF -D WITH_GPHOTO2=OFF \
-D WITH_GIGEAPI=ON -D WITH_GSTREAMER=OFF -D WITH_GTK=ON -D WITH_INTELPERC=OFF -D WITH_IPP=ON \
-D WITH_IPP_A=OFF -D WITH_JASPER=ON -D WITH_JPEG=ON -D WITH_LIBV4L=ON -D WITH_OPENCL=ON \
-D WITH_OPENCLAMDBLAS=OFF -D WITH_OPENCLAMDFFT=OFF -D WITH_OPENCL_SVM=OFF -D WITH_OPENEXR=ON \
-D WITH_OPENGL=OFF -D WITH_OPENMP=OFF -D WITH_OPENNI=OFF -D WITH_PNG=ON -D WITH_PTHREADS_PF=OFF \
-D WITH_PVAPI=OFF -D WITH_QT=ON -D WITH_TBB=ON -D WITH_TIFF=ON -D WITH_UNICAP=OFF \
-D WITH_V4L=ON -D WITH_VTK=OFF -D WITH_WEBP=ON -D WITH_XIMEA=OFF -D WITH_XINE=OFF \
-D WITH_LAPACKE=ON -D WITH_MATLAB=OFF .. && \
make -j $(($(nproc) + 1)) && \
sudo make install

RUN git clone https://github.com/IntelRealSense/librealsense.git
RUN cd librealsense && mkdir build && cd build && \
cmake .. -DBUILD_EXAMPLES=true -DBUILD_PYTHON_BINDINGS=bool:true && \
make -j $(($(nproc) + 1)) && \
make install
