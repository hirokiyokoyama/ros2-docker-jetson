FROM nvcr.io/nvidia/l4t-tensorflow:r32.4.4-tf2.3-py3

RUN apt update && apt install -y locales
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG en_US.UTF-8

RUN apt update && apt install -y curl gnupg2 lsb-release
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -
RUN sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'
RUN apt update && apt install -y ros-eloquent-ros-base

RUN echo '#!/bin/bash\nsource /opt/ros/eloquent/setup.bash\nexec "$*"' > /entrypoint.sh && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

