FROM osrf/ros:humble-desktop

RUN apt-get update && apt-get install -y tzdata
ENV TZ=Asia/Tokyo

WORKDIR /root/ros2_ws

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -qq -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        vim \
        byobu \ 
        can-utils \ 
        libasio-dev \
        ros-humble-tf2-geometry-msgs \
    && rm -rf /var/lib/apt/lists/* \
    && apt clean

ADD overlay_ws /root/ros2_ws/src

WORKDIR /root/ros2_ws/src

RUN . /opt/ros/humble/setup.sh \
    && git clone https://github.com/harry3doz/tracer_ros2.git -b humble \
    && cd .. && colcon build

RUN echo "source /opt/ros/humble/setup.bash" >> /etc/bash.bashrc \
    && echo "source /root/ros2_ws/install/setup.bash" >> /etc/bash.bashrc