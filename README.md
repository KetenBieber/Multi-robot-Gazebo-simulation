*use catkin-tools to build the package*

# step1: create a catkin workspace
```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin build
cd ./src
git clone https://github.com/KetenBieber/Multi-robot-Gazebo-simulation.git
cd ../
rosdepc install --from-paths . --ignore-src
catkin build
```
# step2: run the simulation
Of course,you should make sure that u have install the gazebo and rviz
```bash
sudo apt-get install ros-noetic-gazebo
sudo apt-get install ros-noetic-rviz
sudo apt-get install ros-noetic-ros-control
sudo apt-get install ros-noetic-ros-controllers
sudo apt-get install ros-noetic-gazebp-ros-control 
```
then after the catkin build,source your workspace and run the simulation
```bash
mon launch joint_controller single_display.launch

```
this will launch the gazebo and rviz, and you can see only one robot in the gazebo and the joint state in the rviz

```bash
mon launch joint_controller more_display.launch
```
this will spawn two robots in the gazebo and the joint state in the rviz

# step3: control the robot
```bash
rqt
```
then choose the plugin "controller_manager",and start the controller
```bash
cd catkin_ws
source ./devel/setup.bash
rostopic list |grep joint
rostopic pub /joint1_position_controller/command std_msgs/Float64 "data: 3.14"
```
Then the joint can move to the position of pi