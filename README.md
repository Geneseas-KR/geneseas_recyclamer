# recyclamerunlp

Pasos a seguir para poder instalar y ejecutar el simulador.

Ejecutar los siguientes comandos en la terminal

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

Crear una carpeta donde se va a encontrar el codigo y moverse a ella. Para luego clonar el repositorio

```
mkdir ~/recyclamer
mkdir ~/recyclamer/src
cd ~/recyclamer/src
git clone git@github.com:robotrecyclamer/recyclamer.git
```
Agregamos el submodulo del repositorio de hector_gazebo_plugins
```
git submodule update --init --recursive
```

Y ahora para hacer el build y correr la plataforma

```
source /opt/ros/noetic/setup.bash
cd ~/recyclamer
catkin_make
source ~/recyclamer/devel/setup.bash

roslaunch vrx_gazebo vrx.launch
```

Y deberias poder correr el simulador.
