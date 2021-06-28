# Use Turtlebot3 with SLAM approach
Run Turtlebot3 robot with SLAM approach to create a map and save it using ROS meoldic.<br> </br>

**We need first to update & upgeade by run these commands to install ROS 1 if you dosen't installed before :**  
```
$sudo apt update
$sudo apt upgrade
```

<h2>Install ROS 1 </h2>

*Install it via run: **
```
wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_melodic.sh
$ chmod 755 ./install_ros_melodic.sh 
$ bash ./install_ros_melodic.sh 
``` 

**Now, Insatll Dependencies of ROS 1 Packages :** 

```
$ sudo apt-get install ros-melodic-joy ros-melodic-teleop-twist-joy 
ros-melodic-teleop-twist-keyboard ros-melodic-laser-proc 
ros-melodic-rgbd-launch ros-melodic-depthimage-to-laserscan 
ros-melodic-rosserial-arduino ros-melodic-rosserial-python 
ros-melodic-rosserial-server ros-melodic-rosserial-client 
ros-melodic-rosserial-msgs ros-melodic-amcl ros-melodic-map-server ros-melodic-move-base ros-melodic-urdf 
ros-melodic-xacro ros-melodic-compressed-image-transport ros-melodic-rqt* 
ros-melodic-gmapping ros-melodic-navigation ros-melodic-interactive-markers

```
**Second, Install TurtleBot3 Packages :** 
```
$ sudo apt-get install ros-melodic-dynamixel-sdk
$ sudo apt-get install ros-melodic-turtlebot3-msgs
$ sudo apt-get install ros-melodic-turtlebot3
```

**Third, Set TurtleBot3 Model Name by run :** 

```
$ echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
```
**Note : I chose the TurtleBot3 Burger. If you want a TurtleBot3 Waffle Pi, run:**

```
$ echo "export TURTLEBOT3_MODEL=waffle_pi" >> ~/.bashrc
```

<h2> Install Simulation Package </h2>

The TurtleBot3 Simulation Package requires turtlebot3 and turtlebot3_msgs packages to launch the simulation. Its a must.
```
$ cd ~/catkin_ws/src/
$ git clone -b kinetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/catkin_ws && catkin_make
```

There are three Gazebo simulation environments for TurtleBot3 :  

* Empty World
* TurtleBot3 World
* TurtleBot3 House

but for creating a map with SLAM, its better use eathir TurtleBot3 World nor TurtleBot3 House 

So here, i use  TurtleBot3 World to load the Gazebo environment.


```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

**The Output of this commands will be in gazebo like this :**

<img width="700" alt="Gazebo enviroment" src="https://user-images.githubusercontent.com/43522153/123654017-57ee4a00-d836-11eb-97c5-0ab0a23db295.png">

**Note : if your model is waffle or waffle_pi change the TURTLEBOT3_MODEL=burger in above command, to your model.**


<h2> Run SLAM Node : </h2> 
To run slam node, which Gmapping SLAM method is used by default run these command to be launch in Rviz.

```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```
**The Output of the slam of this commands will be in Rviz like this :** <br> </br>

<img width="700" alt="Run slam (Rviz)" src="https://user-images.githubusercontent.com/43522153/123686636-ab718f80-d858-11eb-9ef9-71fd19080814.png">


<h2> Run Teleoperation Node </h2> 

Here to move the robot around, by teleop node using keyboard:
```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```


**This the output of commands to control the robot motion via keyboard :**

<img width="700" alt="KeyboardController" src="https://user-images.githubusercontent.com/43522153/123683550-04d7bf80-d855-11eb-8652-7e454fcf0a91.png">


**The result of Move the robot by this teleop node using keyboard will be like this :**


<image src = "https://user-images.githubusercontent.com/43522153/123684074-afe87900-d855-11eb-9499-6e24e21bc83b.gif" width="700" />


<h2> Save map </h2>

To Save your map, run :
``` 
$ rosrun map_server map_saver -f ~/test_map
```

<img width="700" alt="map gpm" src="https://user-images.githubusercontent.com/43522153/123686249-461d9e80-d858-11eb-8033-fb02ec8a3337.png">

Its will be saved as pgm extension.




