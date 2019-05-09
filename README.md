If this is your first time, please check the [Wiki page](https://github.com/bu-air-lab/UR5e_arm/wiki) of this repository to learn how to work with the arm <br />


----------------------------------------------------------------------------------------------------------------

If ROS is installed but it is first time you are using your current laptop to work with the arm, <br />

`echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc` <br />
`source ~/.bashrc` <br />

Now, go ahead and isntall the libraries below:

`sudo apt-get install ros-kinetic-moveit && sudo apt-get install ros-kinetic-ros-control ros-kinetic-ros-controllers && sudo apt-get install ros-kinetic-industrial-msgs && rosdep install robotiq_modbus_tcp && sudo apt-get install ros-kinetic-soem` <br />

Create a catkin workspace by running the commands below: <br />

`mkdir –p ~/catkin_ws/src <br />
cd catkin_ws <br />
catkin_make <br />
cd ~/catkin_ws/src <br />
git clone https://github.com/bu-air-lab/universal_robot.git <br />
cd ~/catkin_ws/src <br />
git clone https://github.com/bu-air-lab/robotiq.git <br />
cd ~/catkin_ws/src <br />
git clone https://github.com/bu-air-lab/ur_modern_driver` <br />

Now compile: <br />
`cd ~/catkin_ws <br />
catkin_make`

If there are no errors, the source the workspace and run the bringup: <br />
`source devel/setup.bash
roslaunch ur_modern_driver ur5e_bringup.launch robot_ip:=IP_OF_ROBOT`<br />
The robot can go move to hard-coded points:<br />
`rosrun ur_modern_driver test_move.py`<br />

Also, usuing RVIZ, you can give goals to the arm. To do that, open up a new terminal and:<br />
`source ~/catkin_ws/devel/setup.bash
roslaunch ur5_e_moveit_config ur5_e_moveit_planning_execution.launch`<br />

and in another terminal:<br />
`source ~/catkin_ws/devel/setup.bash
roslaunch ur5_e_moveit_config moveit_rviz.launch config:=true`<br />

To work with the gripper:

`sudo usermod -a -G dialout $USER <br />
dmesg | grep tty <br />
sudo chmod 777  /dev/ttyACM0 <br />
rosrun robotiq_2f_gripper_control Robotiq2FGripperRtuNode.py /dev/ttyACM0 `<br />
And in a new terminal:

`rosrun robotiq_2f_gripper_control Robotiq2FGripperSimpleController.py` <br />


Once you are done working, please turn off the arm.





