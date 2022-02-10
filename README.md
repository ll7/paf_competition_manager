# Competition Manger

based on [paf/paf_competition_manager at main · ll7/paf](https://github.com/ll7/paf/tree/main/paf_competition_manager).

A first draft for the implementation for the final competition in the autonomous driving internship (PAF).

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


## Start

### start carla server
   - `cd ~/carla0.9.10.1`
   - `./CarlaUE4.sh`

### load town

```python
import carla
client = carla.Client('localhost', 2000)
client.set_timeout(10.0) # seconds
world = client.load_world('Town05')
```

### source workspace

`source ~/catkin_ws/devel/setup.bash`

### start ego vehicle
   - `roslaunch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch vehicle_filter:=model3`
1. load start and goal yaml file to rosparam
   - [how to load a yaml file](config/How_to_load_yaml.md)
   - `rosparam load config/Town05/town05_sg2.yaml`
2. start set_position server
   - `rosrun paf_competition_manager set_position_server.py`
3. request setting position
   - `rosrun paf_competition_manager set_position_client.py`
4. `rosrun paf_competition_manager simple_competition_manager.py`
5. spawn npcs

```shell
cd carla0.9.10.1/PythonAPI/examples/
python spawn_npc.py -n 200 -w 0
```

9. `rosparam set /competition/traffic_rules false`
10. `rosparam set /competition/ready_for_ego true`

## manual position set

```shell
rostopic pub /carla/ego_vehicle/initialpose geometry_msgs/PoseWithCovarianceStamped "header:
  seq: 0
  stamp:
    secs: 0
    nsecs: 0
  frame_id: ''
pose:
  pose:
    position: {x: 154.44, y: -30.51, z: 0.0}
    orientation: {x: 0.0, y: 0.0, z: 0.0, w: 0.0}
  covariance: [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
    0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0,
    0.0, 0.0, 0.0, 0.0, 0.0, 0.0]" -1
```

## TODO

- create roslaunch file for which loads params and start position server
- improve spawn_npc such that the seed is deterministic