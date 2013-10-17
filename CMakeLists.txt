cmake_minimum_required(VERSION 2.8.3)
project(pointcloud_to_laserscan)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(
    catkin REQUIRED COMPONENTS 
    sensor_msgs nodelet
    pcl_ros pcl_conversions 
    dynamic_reconfigure roscpp
)

generate_dynamic_reconfigure_options(cfg/CloudScan.cfg)

# make sure configure headers are built before any node using them

catkin_package(
  INCLUDE_DIRS 
  LIBRARIES cloud_to_scan
  CATKIN_DEPENDS sensor_msgs nodelet pcl_ros pcl_conversions dynamic_reconfigure roscpp
  DEPENDS system_lib
)

include_directories(${catkin_INCLUDE_DIRS})
link_libraries(${catkin_LIBRARIES})

# Build
add_library(cloud_to_scan src/cloud_to_scan.cpp src/cloud_throttle.cpp)
add_dependencies(cloud_to_scan ${PROJECT_NAME}_gencfg)


