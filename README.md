If this is your first time, please check the [Wiki page](https://github.com/bu-air-lab/UR5e_arm/wiki) of this repository to learn how to work with the arm <br />


----------------------------------------------------------------------------------------------------------------

If ROS is installed on Ubuntu 16.04 but it is first time you are using your current laptop to work with the arm, <br />
```
echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
Now, go ahead and isntall the libraries below:
```
$ sudo apt-get install ros-kinetic-moveit && sudo apt-get install ros-kinetic-ros-control ros-kinetic-ros-controllers && sudo apt-get install ros-kinetic-industrial-msgs && rosdep install robotiq_modbus_tcp && sudo apt-get install ros-kinetic-soem
```
Create a catkin workspace by running the commands below: <br />
```
mkdir -p ~/catkin_ws/src
cd catkin_ws
wstool init src https://raw.githubusercontent.com/bu-air-lab/UR5e_arm/master/rosinstall/kinetic.rosinstall
```
Now compile: <br />
``` 
catkin_make
```
If there are no errors, the source the workspace and run the bringup: <br />
```
source devel/setup.bash
roslaunch ur_modern_driver ur5e_bringup.launch robot_ip:=IP_OF_ROBOT
```
The robot can go move to hard-coded points:<br />
```
rosrun ur_modern_driver test_move.py
```
Also, usuing RVIZ, you can give goals to the arm. To do that, open up a new terminal and:<br />
```
source ~/catkin_ws/devel/setup.bash
roslaunch ur5_e_moveit_config ur5_e_moveit_planning_execution.launch
```

and in another terminal:<br />
```
source ~/catkin_ws/devel/setup.bash
roslaunch ur5_e_moveit_config moveit_rviz.launch config:=true
```
To work with the gripper:

```
sudo usermod -a -G dialout $USER 
dmesg | grep tty 
sudo chmod 777  /dev/ttyACM0 
rosrun robotiq_2f_gripper_control Robotiq2FGripperRtuNode.py /dev/ttyACM0 `
```
And in a new terminal:
```
rosrun robotiq_2f_gripper_control Robotiq2FGripperSimpleController.py 
```

Once you are done working, please turn off the arm.





