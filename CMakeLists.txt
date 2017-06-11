cmake_minimum_required(VERSION 2.8.3)
project(ur_kinematics)

add_compile_options(-std=c++11)

find_package(catkin REQUIRED COMPONENTS roscpp geometry_msgs  pluginlib tf_conversions)

find_package(Boost REQUIRED COMPONENTS system)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES   ur5_kin
  CATKIN_DEPENDS roscpp geometry_msgs moveit_core moveit_kinematics moveit_ros_planning
    pluginlib tf_conversions
  DEPENDS Boost
)


###########
## Build ##
###########

include_directories(SYSTEM ${Boost_INCLUDE_DIR})
include_directories(include ${catkin_INCLUDE_DIRS})

add_library(ur5_kin src/ur_kin.cpp)
set_target_properties(ur5_kin PROPERTIES COMPILE_DEFINITIONS "UR5_PARAMS")



add_executable(ur_inverse_test src/ur_inverse_test.cpp)
 
target_link_libraries(ur_inverse_test  ${catkin_LIBRARIES}  ur5_kin)


#############
## Install ##
#############

install(TARGETS  ur5_kin    ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# install header files
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)
