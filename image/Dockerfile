FROM ros2-jetson-colcon as base

RUN apt update && apt install -y libopencv-dev libboost-python-dev

RUN git clone -b ros2 https://github.com/ros-perception/vision_opencv.git
WORKDIR /colcon_ws
RUN . /opt/ros/eloquent/setup.sh && . /colcon_ws/install/setup.sh && colcon build

FROM ros2-jetson
COPY --from=base /colcon_ws/install /opt/ros/vision_opencv

RUN apt update && apt install -y python3-opencv
ENV LD_PRELOAD /usr/lib/aarch64-linux-gnu/libgomp.so.1

RUN echo '#!/bin/bash\n' > /entrypoint.sh && \
    echo 'source /opt/ros/eloquent/setup.bash\n' >> /entrypoint.sh && \
    echo 'source /opt/ros/vision_opencv/setup.bash\n' >> /entrypoint.sh && \
    echo 'exec "$*"' >> /entrypoint.sh && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

