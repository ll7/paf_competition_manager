# How to save locations

Manual on how to save locations.

Check the install instructions.

## Start the carla server

```bash
cd <carla-directory>
./CarlaUE4.sh
./CarlaUE4.sh -opengl
```

## Load town

```python
$ python
import carla
client = carla.Client('localhost', 2000)
client.set_timeout(10.0) # seconds
world = client.load_world('Town05')
```

## Source workspace

```bash
source <catkin_ws>/devel/setup.bash
```

## Start ego vehicle

```bash
roslaunch carla_ros_bridge carla_ros_bridge_with_example_ego_vehicle.launch vehicle_filter:=model3
```

## start save_position_server

New terminal:

```bash
source <catkin_ws>/devel/setup.bash
rosrun paf_competition_manager save_position_server.py
```

## drive to position

use the manual control to drive to the position

## save position

New terminal:

```bash
source <catkin_ws>/devel/setup.bash
rosrun paf_competition_manager save_position_client.py
```

## manually copy paste the position in the template for the town
