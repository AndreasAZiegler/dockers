FROM osrf/ros:melodic-desktop

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
RUN apt update && apt install -y curl gnupg2 lsb-release

RUN curl http://repo.ros2.org/repos.key | apt-key add -

RUN sh -c 'echo "deb [arch=amd64,arm64] http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'

RUN apt-get update && apt-get install -y \
  git cmake cmake-curses-gui gcc g++ gdb clang clang-tidy clang-tools \
  ros-$ROS_DISTRO-desktop \
  ros-$ROS_DISTRO-ros1-bridge \
  ros-$ROS_DISTRO-ros2bag* ros-$ROS_DISTRO-rosbag2* \
  python3-colcon-common-extensions \
  python3-argcomplete \
  build-essential \
  libgtest-dev \
  lcov \
  libgoogle-glog-dev

RUN cd /usr/src/gtest && cmake . && make && cp *.a /usr/lib

#ENTRYPOINT ["source", "/opt/ros/$CHOOSE_ROS_DISTRO/setup.bash"]
