#FROM nvcr.io/nvidia/l4t-tensorflow:r32.4.4-tf2.3-py3
FROM python:3.6.9

RUN apt update && apt install -y curl lsb-release
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | apt-key add -
RUN sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'
#RUN apt update && apt install -y ros-eloquent-ros-base
RUN apt update && apt install -y python3-colcon-common-extensions git

