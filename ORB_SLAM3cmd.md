######## ORB SLAM ########
## open terminal 1
source ~/.bashrc
roscore

## open terminal 2
source ~/.bashrc
export LD_LIBRARY_PATH=/home/linuxlaitang/ORB_SLAM3/lib/:$LD_LIBRARY_PATH
cd ~/ORB_SLAM3
rosrun ORB_SLAM3 RGBD Vocabulary/ORBvoc.txt Examples/RGB-D/RealSense_D435i.yaml

# How to build orb_slam3
cd ORB_SLAM3
chmod +x build.sh
./build.sh
# build Ros thing
chmod +x build_ros.sh
./build_ros.sh

## open terminal 3
roslaunch realsense2_camera rs_camera.launch 
roslaunch realsense2_camera rs_camera.launch enable_gyro:=true enable_accel:=true enable_infra1:=true enable_infra2:=true unite_imu_method:=linear_interpolation infra_width:=848 infra_height:=480 infra_fps:=30



## check env parametes
printenv | grep ROS

	## should looks like below
	ROS_VERSION=1
	ROS_PYTHON_VERSION=3
	ROS_PACKAGE_PATH=/home/linuxlaitang/orb_WS/src:/home/linuxlaitang/orb_ws/src:/opt/ros/noetic/share
	ROSLISP_PACKAGE_DIRECTORIES=/home/linuxlaitang/orb_WS/devel/share/common-lisp:/home/linuxlaitang/orb_ws/devel/share/common-lisp
	ROS_ETC_DIR=/opt/ros/noetic/etc/ros
	ROS_MASTER_URI=http://localhost:11311
	ROS_ROOT=/opt/ros/noetic/share/ros
	ROS_DISTRO=noetic

######## Grid map cmd ########
# point cloud map to grid map
source /home/linuxlaitang/catkin_ws/devel/setup.bash
roslaunch /home/linuxlaitang/catkin_ws/src/pcd2pgm_package/pcd2pgm/launch/run.launch
#save the map [Need to cd tha location that u wanna save the grid map]
cd /home/linuxlaitang/ORB_SLAM3/map
rosrun map_server map_saver

#A*
source ~/A_star_ws/devel/setup.bash
roslaunch grid_map_search astar_demo.launch




The point cloud map will store under the directory: ~/ORB_SLAM3/map
The catkin_ws include
1. librealsense
2. pointcloud map to grid map
	同时在原pcd文件夹下，也保存了直通滤波和半径滤波后的pcd文件。
	
	
	
######## fast-planner ########
source ~/obj-avoid/devel/setup.bash
## launch rviz window
roslaunch plan_manage rviz.launch
## launch planner
roslaunch plan_manage kino_replan.launch	
	

######## ssh ######## 
## ssh connection init (rerun every time after reboot ) 
systemctl start ssh
## check ssh status 
systemctl status ssh
	


