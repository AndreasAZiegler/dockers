# This is an auto generated Dockerfile for ros:desktop-full
# generated from docker_images/create_ros_image.Dockerfile.em
FROM osrf/ros:melodic-desktop-full-bionic

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
  cmake ccache g++ gcc libc6 git vim pkg-config sudo unzip wget software-properties-common \
  ros-melodic-imu-filter-madgwick ros-melodic-rtabmap-ros ros-melodic-robot-localization
  
# Add librealsense repo
RUN apt-key adv --keyserver keys.gnupg.net --recv-key C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key C8B3A55A6F3EFCDE
RUN add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo bionic main" -u
RUN apt-get install -y librealsense2*
