# recyclamerunlp

Steps to follow to install and run the simulator

Run the following commands in the terminal

```
sudo apt update
sudo apt full-upgrade

sudo apt install -y build-essential cmake cppcheck curl git gnupg libeigen3-dev libgles2-mesa-dev lsb-release pkg-config protobuf-compiler qtbase5-dev python3-dbg python3-pip python3-venv ruby software-properties-common wget 
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
sudo apt update
DIST=noetic
GAZ=gazebo11
sudo apt install ${GAZ} lib${GAZ}-dev ros-${DIST}-gazebo-plugins ros-${DIST}-gazebo-ros ros-${DIST}-hector-gazebo-plugins ros-${DIST}-joy ros-${DIST}-joy-teleop ros-${DIST}-key-teleop ros-${DIST}-robot-localization ros-${DIST}-robot-state-publisher ros-${DIST}-joint-state-publisher ros-${DIST}-rviz ros-${DIST}-ros-base ros-${DIST}-teleop-tools ros-${DIST}-teleop-twist-keyboard ros-${DIST}-velodyne-simulator ros-${DIST}-xacro ros-${DIST}-rqt ros-${DIST}-rqt-common-plugins
```

Create a folder where the code will be located and navigate to it. Then clone the repository.


```
mkdir ~/recyclamer
mkdir ~/recyclamer/src
cd ~/recyclamer/src
git clone https://github.com/robotrecyclamer/recyclamer.git
```

And now to build and run the platform.

```
source /opt/ros/noetic/setup.bash
cd ~/recyclamer
catkin_make
source ~/recyclamer/devel/setup.bash

roslaunch vrx_gazebo vrx.launch
```

And you should be able to run the simulator.


OBSERVATIONS:
1) This simulator is designed for kinematics tests of the Geneseas Recyclamer robot. Dynamics tests will not reflect behaviors that are 100% consistent with the real robot.
2) The sensor topics are in accordance with those used on the real robot.
3) For the motor topics, the original names from the VRX simulator (/wamv/thrusters/...) are used. When using codes on the real robot, we can use the remap tool:
```
      <!-- uncomment to use with the real robot-->
      <?ignore
      <remap from="/wamv/thrusters/left_thrust_cmd" to="/geneseas/motor_l"/>
      <remap from="/wamv/thrusters/right_thrust_cmd" to="/geneseas/motor_r"/>
      <remap from="/wamv/thrusters/middle_thrust_cmd" to="/geneseas/motor_c"/>
      <remap from="/wamv/thrusters/direction_thrust_cmd" to="/geneseas/motor_d"/>
      ?>
```
4) The default world is located in the Sydney regatta, so take this into account in the localization codes to be tested (UTM zone and magnetic declination)
