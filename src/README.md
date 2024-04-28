# Roboost Cortex - Packages

Based on

- [Articulated Robotics](https://www.youtube.com/watch?v=CwdbsvcpOHM&ab_channel=ArticulatedRobotics)
- [Mobile Robot URDF blogpost](https://medium.com/teamarimac/create-a-mobile-robot-model-with-ros-urdf-4dc46446db7f)
- [ROS2 Docs](https://docs.ros.org/en/humble/index.html)

## Installation

To install the packages, run the following command in the root of the workspace:

```bash
rosdep install -i --from-path src --rosdistro humble -y
colcon build
```

Then source the workspace:

```bash
source install/local_setup.bash
```

## Packages

### roboost

TODO: add description

#### launch files

##### camera.launch.py

This launch file will launch the camera node. This is needed to publish the camera stream and to make the camera available to other nodes.

```bash
ros2 launch roboost camera.launch.py
```

##### joy_control.launch.py

This launch file will launch the joy_control node. This is needed to control the robot with a joystick.

```bash
ros2 launch roboost joy_control.launch.py
```

###### mecanum_sim.launch.py

If you do not have a robot, you can launch the mecanum_sim.launch.py file to launch the robot in Gazebo. This will also launch the mecanum_tf_broadcast.

```bash
ros2 launch roboost mecanum_sim.launch.py world:=src/roboost/worlds/home.world
```

##### mecanum_tf_broadcast.launch.py

This launch file will launch the robot_state_publisher and the odom_to_base_node. This is needed to publish the tf tree for the robot and to make the urdf model available to other nodes.

```bash
ros2 launch tf_broadcast_package mecanum_tf_broadcast_launch.py
```

### [yolov8_ros](https://github.com/mgonzs13/yolov8_ros)

#### Test Usage

To launch the package, run the following commands:

For the camera stream:

```bash
ros2 launch roboost camera.launch.py
```

For the yolov8 node:

```bash
ros2 launch yolov8_bringup yolov8.launch.py device:=cpu input_image_topic:=/image_raw
```

For rqt image view:

```bash
ros2 run rqt_image_view rqt_image_view
```

### [slam-toolbox](https://github.com/SteveMacenski/slam_toolbox)

To start mapping, launch the slam toolbox using the provided config:

```bash
ros2 launch slam_toolbox online_async_launch.py params_file:=./src/roboost/config/mapper_params_online_async.yaml
```

### Workflow

To use AMCL and SLAM Toolbox with Roboost Cortex, follow these steps:

For demonstration purposes, we will use the mecanum_sim.launch.py file to launch the robot in Gazebo. This will also launch the mecanum_tf_broadcast.

```bash
ros2 launch roboost mecanum_sim.launch.py world:=src/roboost/worlds/home.world
```

For controlling the robot with a joystick, launch the joy_control.launch.py file and optionally start the multiplexer:

```bash
ros2 launch roboost joy_control.launch.py
ros2 run twist_mux twist_mux --ros-args --params-file ./src/roboost/config/twist_mux.yaml -r cmd_vel_out:=cmd_vel
```

#### Mapping with SLAM Toolbox

To start mapping, launch the slam toolbox using the provided config:

```bash
ros2 launch slam_toolbox online_async_launch.py params_file:=./src/roboost/config/stb_mapping.yaml
```

The map can be saved within rviz2 by going to Panels -> Add New Panel -> slam_toolbox -> SlamToolboxPlugin. Then you can save the map in the old .pgm format by clicking the "Save Map" button (after giving it a name), or you can save it in the new .yaml format by clicking the "Serialize Map" button (after giving it a name). The map will be saved in the folder where you launched rviz2.

For localization, you can use the stb_localization.yaml config file, however I would recommend using the Nav2 package instead.

#### Localization with Nav2

Once you have a map, you can stop the slam_toolbox node and start the amcl localization node like this (use_sim_time optionally):

```bash
ros2 launch roboost localization_launch.py map:=./src/roboost/maps/home_map.yaml params_file:=./src/roboost/config/nav2_params.yaml #use_sim_time:=true
```

This will start the amcl localization node and the map_server node. Now you can vizualize the map in rviz2 by adding the corresponding topic (usually you also have to set the Durability Policy to Transient Local). You will also need to set the initial pose of the robot in rviz2. This can be done by clicking the "2D Pose Estimate" button and then clicking on the map where the robot is located. The robot will then start localizing itself on the map.

#### Navigation with Nav2

Once you have a map and the robot is localized, you can start the navigation stack like this:

```bash
ros2 launch roboost navigation_launch.py map:=./src/roboost/maps/home_map.yaml map_subscribe_transient_local:=true params_file:=./src/roboost/config/nav2_params.yaml #use_sim_time:=true
```

Now you can send a goal to the robot using rviz2. This can be done by clicking the "2D Nav Goal" button and then clicking on the map where you want the robot to go. The robot will then start navigating to the goal. Note that the costmaps can now also be visualized in rviz2.

### Timescale Connector

The Timescale Connector is a ROS2 node that connects to a TimescaleDB database and publishes ROS2 messages to the database. The topics to be published are specified in the "timescale.yaml" config file.

To run the Timescale Connector, run the following command:

```bash
ros2 run roboost timescale_connector
```

### Image Streamer

To publish a video stream to the /camera topic, run the following command:

```bash
ros2 run roboost image_publisher <video source number>
```

This will utalize the image_transport package to publish the video stream to the /camera topic.

To view the video stream, run the following command:

```bash
ros2 run roboost image_stream --ros-args -p _image_transport:=compressed
```

## TODO

- [ ] Add description to README.md
- [ ] Add robot_localization package
