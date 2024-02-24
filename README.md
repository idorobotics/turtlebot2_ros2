# turtlebot2_ros2
This project contains a minimal example for setting up ROS 2 Humble on the Kobuki [TurtleBot 2 platform](https://www.turtlebot.com/). Teleoperation using the keyboard and a joystick controller is demonstrated. 
For a comprehensive guide, see [idorobotics.com](https://idorobotics.com/2024/02/20/ros2-on-kobuki-turtlebot/).
## Setup
To setup the TurtleBot 2 mobile robot base:
- Install the velocity smoother and sophus packages:
```sudo apt-get install ros-humble-kobuki-velocity-smoother ros-humble-sophus```
- In a ROS 2 workspace, clone this repository (which adds the kobuki_core, kobuki_ros, kobuki_ros_interfaces, cmd_vel_mux, ecl_core and ecl_lite packages):
```git clone https://github.com/idorobotics/turtlebot2_ros2.git```
- Install any missing depencies:
```rosdep install -i --from-path src --rosdistro humble -y```
- Build the workspace
```colcon build --symlink-install --executor sequential```
- Update udev rules, check version information and run the kobuki-simple-keyop test noted in the [official guide](https://kobuki.readthedocs.io/en/release-1.0.x/software.html).
 ## Testing
 To test this setup, run remote teleoperation to control (drive around) the robot from a workstation (laptop) computer following the steps below:
 - Install the teleop packages:
 ```sudo apt-get install ros-humble-teleop-twist-keyboard ros-humble-joy-teleop ros-humble-teleop-twist-joy```
 - Open an ssh connection to the robot then start the robot:
 ```ros2 launch kobuki_node kobuki_node-launch.py```
 - Run keyboard teleoperation (to drive the robot using a keyboard):
 ```ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args --remap cmd_vel:=commands/velocity```
 - Alternatively, run joystick teleoperation (to drive the robot using a joystick):
 ```ros2 launch teleop_twist_joy teleop-launch.py config_filepath:='/path/to/ros2_ws/src/configs/pdp.config.yaml' joy_vel:='commands/velocity'```

   If you're using a different joystick like PS3 then run:
```ros2 launch teleop_twist_joy teleop-launch.py joy_config:='ps3' joy_vel:='commands/velocity'```

The Kobuki TurtleBot 2 is now fully migrated to ROS 2 and is ready for more complex navigation tasks. 
