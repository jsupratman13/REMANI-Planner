cmake_minimum_required(VERSION 2.8.3)
project(mm_config)

set(CMAKE_BUILD_TYPE "Release")
ADD_COMPILE_OPTIONS(-std=c++14 )

find_package(Eigen3 REQUIRED)
find_package(OpenCV REQUIRED)
find_package(PCL REQUIRED)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  roslib
  std_msgs
  visualization_msgs
  plan_env
)

catkin_package(
 INCLUDE_DIRS include
 LIBRARIES mm_config
 CATKIN_DEPENDS plan_env
 DEPENDS OpenCV
)

include_directories(
    SYSTEM
    include
    ${catkin_INCLUDE_DIRS}
    ${EIGEN3_INCLUDE_DIRS}
    ${OPENCV_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
)

#add_message_files{
#    FILES
#    Assignment.msg
#}

add_library( mm_config
    src/mm_config.cpp
    )

target_link_libraries( mm_config
    ${catkin_LIBRARIES}
    ${OpenCV_LIBRARIES}
    ${PCL_LIBRARIES}
    )
