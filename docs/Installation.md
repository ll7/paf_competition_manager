# Installation

How to install the `paf_competition_manager` package.

## Prerequisites

carla0.9.10.1 installation

carla_ros_bridge@0.9.10.1 installation

## Clone, Link, Build

### Clone

clone the repository to a desired location

   - `git clone https://github.com/ll7/paf_competition_manager.git`

### Link

   - create a symbolic link from the package to you workspace src folder. Example:
     - `ln -s ~/paf_competition_manager ~/catkin_ws/src/`
   - Substitute `~` with your actual folder locations


### Build

`catkin_make`

#### optional: use `catkin build` instead of `catkin_make`

Reason: https://robotics.stackexchange.com/questions/16604/ros-catkin-make-vs-catkin-build

installation for Ubuntu 20.04 and ROS Noetic based on https://answers.ros.org/question/353113/catkin-build-in-ubuntu-2004-noetic/

`sudo apt install python3-catkin-tools python3-osrf-pycommon`

`catkin build`