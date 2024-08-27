# Use the official ROS 2 Jazzy base image
FROM osrf/ros:jazzy-desktop

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive
ENV ROS_DISTRO=jazzy

# Install necessary packages and dependencies
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y \
    curl \
    gnupg2 \
    lsb-release \
    build-essential \
    python3-pip \
    python3-colcon-common-extensions \
    python3-colcon-mixin \
    python3-vcstool \
    git \
    wget \
    vim \
    nano \
    less \
    ros-jazzy-turtlesim \
    ros-jazzy-geometry-msgs \
    ros-jazzy-rviz2 && \
    apt-get install -y python3-rosdep

# Initialize rosdep and handle existing sources list
RUN rm -rf /etc/ros/rosdep/sources.list.d/20-default.list && \
    rosdep init && \
    rosdep update

# Create a colcon workspace and clone the rmw_zenoh repository
RUN mkdir -p /root/ws_rmw_zenoh/src && \
    cd /root/ws_rmw_zenoh/src && \
    git clone https://github.com/ros2/rmw_zenoh.git

# Install dependencies using rosdep
RUN cd /root/ws_rmw_zenoh && \
    rosdep install --from-paths src --ignore-src --rosdistro $ROS_DISTRO -y

# Source ROS 2 setup script and build the workspace
RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash && \
    cd /root/ws_rmw_zenoh && \
    colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release && \
    source install/setup.bash"

# Set Zenoh as the default RMW implementation
RUN echo "source /root/ws_rmw_zenoh/install/setup.bash" >> /root/.bashrc && \
    echo "export RMW_IMPLEMENTATION=rmw_zenoh_cpp" >> /root/.bashrc

# Set the working directory to the absolute path
WORKDIR /root/ws_rmw_zenoh

# Install NVIDIA software
RUN apt-get update \
 && apt-get -y --quiet --no-install-recommends install \
    libglvnd0 \
    libgl1 \
    libglx0 \
    libegl1 \
    libxext6 \
    libx11-6 \
  && rm -rf /var/lib/apt/lists/*
ENV NVIDIA_VISIBLE_DEVICES=all
ENV NVIDIA_DRIVER_CAPABILITIES=graphics,utility,compute
ENV QT_X11_NO_MITSHM=1

# Default command to run
CMD ["bash"]
