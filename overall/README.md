# GRASPFLOW with ROS instructions

## ROBOT (Panda Emika Franka)

###  Prerequisits
1. Install [Libfranka](https://github.com/frankaemika/libfranka/tree/80197c6f57d87e4a4d0fe298e89107ab46543808) using [Franka Control Interface Documentation](https://frankaemika.github.io/docs/).
2. Install modified [franka_ros](https://github.com/tasbolat1/franka_ros). Note if you recursively install first step, ignore this one.
3. Run in catkin_graspflow root:

    ``catkin_make -DCMAKE_BUILD_TYPE=Release -DFranka_DIR:PATH=/home/crslab/libfranka/build``

4. At this moment,

(i)  check that robot is connectable and reachable by ros commands
Within libfranka/build/examples run:

``/.communication_test <robot_ip>``

(ii) run move_robot

``rosrun graspflow move_robot_new.git``

(iii) check that robot infact moves by rostopic command:

``rostopic pub -1 /move_to std_msgs/String "data: '1 1 [[0, 0], [0.52578, 0.0424, 0.3175], [0.99884, -0.0237, -0.0415, -0.0053]]'"``

If all above is working, then robot part is installed properly.

## CV (Realsense D435i)

###  Prerequisits
1. Install (realsense sdk)[https://github.com/IntelRealSense/librealsense]
2. realsense-ros is already as submodule within catkin_graspflow (please checkout to 2.3.1 tag and development branch using fetch and checkout).
3. Install pcl and it's python bindings respectively.
3. To run vision:

``roslaunch realsense2_camera rs_rgbd.launch ``

4. To run vision:

in new terminal 

``rosrun pclanager pcl_segmentor.py``

in new terminal

``rosrun pcl_manager pcl_managerypy``



### TROUBLESHOOTS ###

1. For robot pc, remove cv related packages or do not catkin make them

catkin_make -DCATKIN_BLACKLIST_PACKAGES="realsense2_camera;realsense2_description" -DCMAKE_BUILD_TYPE=Release -DFranka_DIR:PATH=/home/crslab/libfranka/build