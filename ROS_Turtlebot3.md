# Tutorial Basico TurtleBot3
![Badge em Desenvolvimento](http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge)

## Instalação dos pacotes dependentes:
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

## Instalação dos pacotes TurtleBot3:
```
$ sudo apt install ros-noetic-dynamixel-sdk
$ sudo apt install ros-noetic-turtlebot3-msgs
$ sudo apt install ros-noetic-turtlebot3
```

Download do gazebo_ros_pkgs:

Gazebo:

```
$ sudo apt-get install -y libgazebo11-dev
```

```
$ cd ~/catkin_ws/src
$ git clone https://github.com/ros-simulation/gazebo_ros_pkgs.git -b noetic-devel
```

Checar as dependências com rosdep:
```
$ rosdep update
$ rosdep check --from-paths . --ignore-src --rosdistro noetic
$ rosdep install --from-paths . --ignore-src --rosdistro noetic -y
```
![image](https://user-images.githubusercontent.com/112727443/235547039-f7d0fba3-fa35-460a-b846-ca851c26b3e7.png)

Compilando a workspace:
```
$ cd ~/catkin_ws/
$ catkin_make
```

## Instalação dos pacotes de Simulação do TurtleBot3:

```
$ cd ~/catkin_ws/src
$ git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/catkin_ws && catkin_make
```

## Simulação no Gazebo

Para iniciar a simulação, iniciamos o roscore:
```
$ cd ~/catkin_ws
$ roscore
```
Em outro terminal, iniciamos o TurtleBot3 World:
```
$ source devel/setup.bash
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_gazebo turtlebot3_house.launch
```

![image](https://user-images.githubusercontent.com/112727443/235548948-47cfe424-74cc-4f44-9ddf-a416a247c565.png)

Em outro terminal, iniciamos o nodo de teleoperação:
```
$ source devel/setup.bash
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
![](https://github.com/HerickDallAgnol/ROS_workshop/blob/main/turlebot1teleop.gif)

# Simulação SLAM 

O SLAM (Simultaneous Localization and Mapping) é uma técnica para desenhar um mapa estimando a localização atual em um espaço arbitrário.

## Mapeamento

Iniciamos o Roscore:
```
$ cd catkin_ws
$ roscore
```

Iniciamos o TurtleBot3 World:
```
$ source devel/setup.bash
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

Em outro terminal rodamos a teleoperação:
```
$ source devel/setup.bash
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

Em um novo terminal rodamos o gmapping:
```
$ source devel/setup.bash
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
Dicas para criar um bom mapa:
  + Tente dirigir o mais devagar possível.
  + Evite dirigir linearmente e girar ao mesmo tempo.
  + Não dirija muito perto dos obstáculos.

![image](https://user-images.githubusercontent.com/112727443/235554590-34173d73-3c36-4c64-8ea7-e592b1894fb4.png)

## Navegação

Iniciamos o Roscore:
```
$ cd catkin_ws
$ roscore
```

Para navegação devemos abrir o TurtleBot3 World:
```
$ source devel/setup.bash
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
Em outro terminal rodamos o nodo de navegação:
```
$ source devel/setup.bash
$ export TURTLEBOT3_MODEL=waffle
$ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```
<sub>NOTA:map:= "Diretorio aonde foi salvo seu mapa" </sub>

**No rviz:**

Para realizar a navegação autonoma, deve se clicar em ***2D POSE ESTIMATE*** aonde estimamos a posição do nosso robô. Após isso podemos clicar em ***2D NAV GO*** selecionando um local para o robô navegar.

![](https://github.com/HerickDallAgnol/ROS_workshop/blob/main/naveros1.gif)
