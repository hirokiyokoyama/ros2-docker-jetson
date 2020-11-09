#FROM nvcr.io/nvidia/l4t-tensorflow:r32.4.4-tf2.3-py3
FROM ros2-jetson

RUN apt update && apt install -y curl lsb-release
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -
RUN sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'
RUN apt update && apt install -y ros-eloquent-ros-base python3-colcon-common-extensions git
#RUN apt install -y libboost-python-dev
#RUN pip3 install -U pip && pip3 install cmake

RUN mkdir -p /colcon_ws/src
RUN cd /colcon_ws && colcon build
WORKDIR /colcon_ws/src

RUN echo '#!/bin/bash\n' > /entrypoint.sh && \
    echo 'source /opt/ros/eloquent/setup.bash\n' >> /entrypoint.sh && \
    echo 'source /colcon_ws/install/setup.bash\n' >> /entrypoint.sh && \
    echo 'source /colcon_ws/install/local_setup.bash\n' >> /entrypoint.sh && \
    echo 'exec "$*"' >> /entrypoint.sh >> /entrypoint.sh && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

