FROM ubuntu:18.04

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
build-essential \
git \
virtualenv \
python-dev python-pip python-setuptools \
libxml2-dev libxslt1-dev zlib1g-dev \
redis-server

#RUN git clone https://github.com/rtfd/readthedocs.org.git
#RUN cd readthedocs.org

#RUN virtualenv venv
#RUN . venv/bin/activate

#RUN pip install -r readthedocs.org/requirements.txt

#RUN python readthedocs.org/manage.py migrate

#RUN python readthedocs.org/manage.py createsuperuser

#RUN python readthedocs.org/manage.py collectstatic
