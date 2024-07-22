# Turtlebot3 




Enviorment:
  - ROS Distro: Noetic 20.04
  - OS  Version: Ubuntu 20.04.6
  - [Turtlebot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/).
  - Using Gazibo Simulation



***

## What is Turtlebot3 ?
Turtlebot3 is an open-source autonomous mobile robot platform designed for research and education purposes. It was developed by Robotis, a South Korean robotics company, in collaboration with the Robot Operating System (ROS) community.

The Turtlebot3 is a small, lightweight, and affordable robot that can be easily customized and used for various robotics applications, such as:

- **Navigation and mapping**: equipped with sensors like LiDAR, cameras, IMUs to navigate and map its environment.
- **Autonomous exploration**: programmed to autonomously explore and navigate through indoor and outdoor environments.
- **Human-robot interaction**: used to develop applications that involve interaction with humans, e.g. remote telepresence.
- **Research and development**: The open-source nature of the Turtlebot3 allows researchers and developers to modify and experiment with the robot's hardware and software.

  
***

## Turtlebot3 Models

1. Turtlebot3 Burger: The most basic model, designed for beginner users and educational purposes.
2. Turtlebot3 Waffle: A more advanced model with additional sensors and capabilities, suitable for research and development.
3. Turtlebot3 Waffle Pi: A variant of the Turtlebot3 Waffle with a Raspberry Pi4 as the main controller, making it a cost-effective option for education and prototyping.


  <img src="https://github.com/user-attachments/assets/f3062c1d-5f01-4310-a181-da8161eb2a7b" width="210" height="150">

  <img src="https://github.com/user-attachments/assets/1a537e34-30ad-4896-9b90-4db49be62e44" width="210" height="150">



***

## Learn about TrutleBot3

- [ROBOTIS e-Manual](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [Turtulebot3 package](http://wiki.ros.org/turtlebot3)
- [Turtulebot3_simulation package](http://wiki.ros.org/turtlebot3_simulations)




***




# Setup Your Envioremnt

## PC Setup

> Note:
> The contents in this chapter corresponds to the Remote PC (your desktop or laptop PC) which will control TurtleBot3. Do not apply this instruction to your TurtleBot3


1. Install Ubuntu 20.04:
   - Step By Step [How to Install Ubuntu 20.04](https://github.com/alanoudmk/Install-Ubuntu-20.04.6-On-VirtualBox).
     
2. Open a **Terminal**: 
   > Ctrl + Alt + T

3. Install ROS Noetic on Remote PC: 
  - Step By Step [How to Install ROS Noetic 20.04.6](https://github.com/alanoudmk/Install-ROS-Noetic-on-Ubuntu)
  - Or:
```
  $ sudo apt update
  $ sudo apt upgrade
  $ wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_noetic.sh
  $ chmod 755 ./install_ros_noetic.sh 
  $ bash ./install_ros_noetic.sh
```

4. Install Dependent ROS Packages:
```
  $ sudo apt-get install ros-noetic-joy ros-noetic-teleop-twist-joy \
  ros-noetic-teleop-twist-keyboard ros-noetic-laser-proc \
  ros-noetic-rgbd-launch ros-noetic-rosserial-arduino \
  ros-noetic-rosserial-python ros-noetic-rosserial-client \
  ros-noetic-rosserial-msgs ros-noetic-amcl ros-noetic-map-server \
  ros-noetic-move-base ros-noetic-urdf ros-noetic-xacro \
  ros-noetic-compressed-image-transport ros-noetic-rqt* ros-noetic-rviz \
  ros-noetic-gmapping ros-noetic-navigation ros-noetic-interactive-markers
```

5. Install TurtleBot3 Packages:
```
   $ sudo apt install ros-noetic-dynamixel-sdk
   $ sudo apt install ros-noetic-turtlebot3-msgs
   $ sudo apt install ros-noetic-turtlebot3
```


***



# Gazebo Simulation
The [Gazebo Simulation](https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/#gazebo-simulation) is a powerful tool for TurtleBot3 development and testing, as it allows you to experiment with different algorithms, sensors, and behaviors without the risk of damaging the physical robot or the environment. 

## 1. Create ROS1 Noetic Workspace:
If you haven't created the ROS1 Noetic workspace yet, follow these steps:
   
1. Open a **Terminal** & Source the ROS 1 Noetic: 
   > Ctrl + Alt + T
```
  $ source /opt/ros/noetic/setup.bash
  $ echo $ROS_DISTRO
```
  - The output should be "noetic".
  - Create the Workspace Directory:
```
  $ cd
  $ mkdir catkin_ws
```

2. Create The Source Folder & Build the Workspace:  

  ```
    $ cd catkin_ws/
    $ mkdir src
    $ catkin_make
    $ source devel/setup.bash
  ```

3. Source Catkin Workspace: 

 ```
   $ cd devel/
   $ source setup.bash 
  ```

***

## 2. Install Simulation Package:
The TurtleBot3 Simulation Package requires ``turtlebot3`` and ``turtlebot3_msgs`` packages as prerequisite. 

> Note: Without these prerequisite packages, the Simulation cannot be launched.

```
  $ cd ~/catkin_ws/src/
  $ git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
  $ cd ~/catkin_ws && catkin_make
```
***

## 3. Launch Simulation World
Three simulation environments are prepared for TurtleBot3. Please select one of these environments to launch Gazebo.

> Please make sure to completely terminate other Simulation world before launching a new world.

1. Empty World
2. TurtleBot3 World
3. TurtleBot3 House

###  Empty World:
```
  $ export TURTLEBOT3_MODEL=burger
  $ roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch
```

### TurtleBot3 World:
```
  $ export TURTLEBOT3_MODEL=waffle
  $ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

###  TurtleBot3 House:
> NOTE: If TurtleBot3 House is launched for the first time, downloading the map may take more than a few minutes depending the network status.

```
  $ export TURTLEBOT3_MODEL=waffle_pi
  $ roslaunch turtlebot3_gazebo turtlebot3_house.launch
```

## 4. Operate TurtleBot3 
Launch the teleoperation node with below command in a new terminal window.
```
  $ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```




***



# SLAM Simulation
When [SLAM in Gazebo](https://emanual.robotis.com/docs/en/platform/turtlebot3/slam_simulation/) simulator, you can select or create various environments and robot models in virtual world. 
Other than preparing simulation environment instead of bringing up the robot, SLAM Simulation is pretty similar to that of SLAM with the actual TurtleBot3.

> The following instructions require prerequisites from the previous sections, so please review to the Gazebo section first.

### 1.Launch Simulation World
- Three Gazebo environments are prepared, but for creating a map with SLAM, it is recommended to use either ``TurtleBot3 World`` or ``TurtleBot3 House``.
- Please use the proper keyword among ``burger``, ``waffle``, ``waffle_pi`` for the TURTLEBOT3_MODEL parameter.

```
  $ export TURTLEBOT3_MODEL=burger
  $ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

### 2. Run SLAM Node

1. Open a **Terminal** & Source the ROS 1 Noetic: 
   > Ctrl + Alt + T
```
  $ source /opt/ros/noetic/setup.bash
```

2. Run SLAM Node:
  - Gmapping SLAM method is used by default.
```
  $ export TURTLEBOT3_MODEL=burger
  $ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```


### 3. Run Teleoperation Node

1. Open a new **Terminal** & Source the ROS 1 Noetic: 
   > Ctrl + Alt + T
```
  $ source /opt/ros/noetic/setup.bash
```

2. Run Teleoperation Node:
```
  $ export TURTLEBOT3_MODEL=burger
  $ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

3. Control Your TurtleBot3:
 ---------------------------
 Moving around:


- w/x : increase/decrease linear velocity
- a/d : increase/decrease angular velocity
- space key, s : force stop
---------------------------
 
4. To Quit:
 > CTRL + C

  
### 4. Save The Map
When the map is created successfully:

1. Open a **Terminal** & Source the ROS 1 Noetic: 
   > Ctrl + Alt + T
```
  $ source /opt/ros/noetic/setup.bash
```

2. Save the map:
```
  $ rosrun map_server map_saver -f ~/map
```

> The saved map.pgm file


***

# Navigation Simulation
Just like the SLAM in Gazebo simulator, you can select or create various environments and robot models in [virtual Navigation world](https://emanual.robotis.com/docs/en/platform/turtlebot3/nav_simulation/).

Proper map has to be prepared before running the Navigation. Other than preparing simulation environment instead of bringing up the robot, Navigation Simulation is pretty similar to that of Navigation.

### 1. Launch Simulation World

1. Terminate all applications:
  > Ctrl + C 

2. Launch Simulation World
 - In the previous SLAM section, TurtleBot3 World is used to creat a map. The same Gazebo environment will be used for Navigation.
 - Please use the proper keyword among ``burger``, ``waffle``, ``waffle_pi`` for the TURTLEBOT3_MODEL parameter.
 
```
  $ export TURTLEBOT3_MODEL=burger
  $ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```


### 2. Run Navigation Node

1. Open a **Terminal** & Source the ROS 1 Noetic: 
   > Ctrl + Alt + T
```
  $ source /opt/ros/noetic/setup.bash
```

2. Run Navigation Node:
```
  $ export TURTLEBOT3_MODEL=burger
  $ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```


### 3. Estimate Initial Pose

- Initial Pose Estimation
  - must be performed before running the Navigation as this process initializes the AMCL parameters that are critical in Navigation.
  - TurtleBot3 has to be correctly located on the map with the LDS sensor data that neatly overlaps the displayed map.

1. Click the ``2D Pose Estimate`` button in the RViz menu.
    <img src="https://github.com/user-attachments/assets/104fa192-a120-41d9-a257-b571130fcf77" width="460" height="70">



2. Click on the map where the actual robot is located and drag the large green arrow toward the direction where the robot is facing.

3. Repeat step 1 and 2 until the LDS sensor data is overlayed on the saved map.

4. Launch keyboard teleoperation node to precisely locate the robot on the map.
```
  $ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

5. Move the robot back and forth a bit to collect the surrounding environment information and narrow down the estimated location of the TurtleBot3 on the map which is displayed with tiny green arrows.
 
6. Terminate the keyboard teleoperation node:
    > Ctrl + C 

   
### 4. Set Navigation Goal

1. Click the ``2D Nav Goal`` button in the RViz menu.
    <img src="https://github.com/user-attachments/assets/8b08ea67-8cf3-472f-837a-6c0657f1d60b" width="460" height="70">

2. Click on the map to set the destination of the robot and drag the green arrow toward the direction where the robot will be facing.
  - This green arrow is a marker that can specify the destination of the robot.
  - The root of the arrow is x, y coordinate of the destination, and the angle θ is determined by the orientation of the arrow.
  - As soon as x, y, θ are set, TurtleBot3 will start moving to the destination immediately.
