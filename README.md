# Turtlebot3 




Enviorment:
  - ROS Distro: Noetic 20.04
  - OS  Version: Ubuntu 20.04.6
  - [Arduino Robot Arm](https://github.com/smart-methods/arduino_robot_arm) Package
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


## 1. Create ROS1 Noetic Workspace:
> If You have not created it alredy
   
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

## Operate TurtleBot3 
Launch the teleoperation node with below command in a new terminal window.
```
  $ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
