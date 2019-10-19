cmake_minimum_required(VERSION 3.5)
project(velodyne)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(gazebo_ros REQUIRED)
find_package(sensor_msgs REQUIRED)

include_directories(include
)

add_library(velodyne_sensor SHARED velodyne_plugin/velodyne_sensor_plugin.cpp)
ament_target_dependencies(velodyne_sensor rclcpp gazebo_ros sensor_msgs)


if(BUILD_TESTING)
endif()

ament_package()

install(TARGETS
  velodyne_sensor
  DESTINATION lib
  # DESTINATION lib/${PROJECT_NAME}
)

install(DIRECTORY
  models/Velodyne
  DESTINATION $ENV{HOME}/.gazebo/models
)
