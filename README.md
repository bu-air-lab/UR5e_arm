Please check the Wiki page of this repository to learn how to work with the arm <br />

If ROS is installed but it is first time you are using your current laptop to work with the arm, <br />

`echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc` <br />
`source ~/.bashrc` <br />

Now, go ahead and isntall the libraries below:

`sudo apt-get install ros-kinetic-moveit && sudo apt-get install ros-kinetic-ros-control ros-kinetic-ros-controllers && sudo apt-get install ros-kinetic-industrial-msgs && rosdep install robotiq_modbus_tcp && sudo apt-get install ros-kinetic-soem` <br />

Create a catkin workspace by running the commands below: <br />

`mkdir –p ~/catkin_ws/src 
cd catkin_ws
catkin_make
cd ~/catkin_ws/src
git clone https://github.com/bu-air-lab/universal_robot.git
cd ~/catkin_ws/src
git clone https://github.com/bu-air-lab/robotiq.git
cd ~/catkin_ws/src
git clone https://github.com/bu-air-lab/ur_modern_driver` <br />

Now compile: <br />
`cd ~/catkin_ws
catkin_make`

If there are no errors, the source the workspace and run the bringup: <br />
`source devel/setup.bash
roslaunch ur_modern_driver ur5e_bringup.launch robot_ip:=IP_OF_ROBOT`
The robot can go move to hard-coded points:
`rosrun ur_modern_driver test_move.py`

Also, usuing RVIZ, you can give goals to the arm. To do that, open up a new terminal and:
`source ~/catkin_ws/devel/setup.bash
roslaunch ur5_e_moveit_config ur5_e_moveit_planning_execution.launch`

and in another terminal:
`source ~/catkin_ws/devel/setup.bash
roslaunch ur5_e_moveit_config moveit_rviz.launch config:=true`







