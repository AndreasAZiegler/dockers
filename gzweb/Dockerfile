FROM gazebo:libgazebo9-stretch

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

# install packages
RUN apt-get update && apt-get install -q -y \
    build-essential \
    curl \
    cmake \
    imagemagick \
    libboost-all-dev \
    libgts-dev \
    libjansson-dev \
    libtinyxml-dev \
    mercurial \
    pkg-config \
    psmisc \
    xvfb \
    && rm -rf /var/lib/apt/lists/*

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get update && apt-get install -q -y \
    nodejs \
    npm

# install gazebo packages
RUN apt-get update && apt-get install -q -y \
    libgazebo9-dev=9.6.0-1* \
    && rm -rf /var/lib/apt/lists/*

# clone gzweb
ENV GZWEB_WS /root/gzweb
RUN hg clone https://bitbucket.org/osrf/gzweb $GZWEB_WS
WORKDIR $GZWEB_WS

# build gzweb
RUN hg up default \
    && xvfb-run -s "-screen 0 1280x1024x24" ./deploy.sh -m -t

# setup environment
EXPOSE 8080
EXPOSE 7681

# run gzserver and gzweb
CMD gzserver --verbose & npm start
