FROM ros2-jetson

RUN apt update && apt install -y python3-colcon-common-extensions git

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

