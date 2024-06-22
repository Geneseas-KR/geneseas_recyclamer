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
git clone https://github.com/robotrecyclamer/recyclamer.git
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


OBSERVACIONES:
1) Este simulador esta orientado a pruebas de cinematica del robot Geneseas Recyclamer. Prubas de dinamica no reflejaran comportamientos 100% coincidentes con robot real.
2) Los topicos de los sensores estan en acuerdo a los utilizados en el robot real.
3) En los topicos de los motores, se utilizan los nombres originales del simulador VRX (/wamv/thrusters/...). Al utilizarse codigos en el robot real podemos usar la herramienta remap:

```
      <!-- decomentar para usar con robot real-->
      <?ignore
      <remap from="/wamv/thrusters/left_thrust_cmd" to="/geneseas/motor_l"/>
      <remap from="/wamv/thrusters/right_thrust_cmd" to="/geneseas/motor_r"/>
      <remap from="/wamv/thrusters/middle_thrust_cmd" to="/geneseas/motor_c"/>
      <remap from="/wamv/thrusters/direction_thrust_cmd" to="/geneseas/motor_d"/>
      ?>
```
3) El mundo por defecto se ubica en la regata de Sidney por tanto tomar en cuenta en codigos de localizacion a testear (zona UTM y declinacion magnetica)