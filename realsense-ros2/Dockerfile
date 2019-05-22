FROM ros:crystal

ENV DEBIAN_FRONTEND noninteractive

# nvidia-docker hooks
LABEL com.nvidia.volumes.needed="nvidia_driver"
ENV PATH /usr/local/nvidia/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64:${LD_LIBRARY_PATH}
ENV LANG en_US.UTF-8
ENV ROS_DISTRO crystal

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

# Set the locale
RUN apt-get clean && apt-get update && apt-get install -y locales apt-utils
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

# install packages
RUN apt update && apt install -y curl gnupg2 lsb-release software-properties-common

# Add RealSense repo
RUN apt-key adv --keyserver keys.gnupg.net --recv-key C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key C8B3A55A6F3EFCDE
RUN add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo bionic main" -u

RUN apt-get update && apt-get install -y \
  build-essential git cmake cmake-curses-gui gcc g++ gdb clang clang-tidy clang-tools \
  ros-crystal-desktop python3-argcomplete python3-colcon* \
  ros-crystal-cv-bridge ros-crystal-message-filters ros-crystal-image-transport \
  libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev \
  libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev librealsense2*

#ENTRYPOINT ["source", "/opt/ros/$CHOOSE_ROS_DISTRO/setup.bash"]
