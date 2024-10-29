cmake_minimum_required(VERSION 3.5)
project(hipnuc_imu)

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
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)

add_executable(hipnuc_imu_driver src/hipnuc_imu_driver.cpp src/hipnuc_dec.c)
ament_target_dependencies(hipnuc_imu_driver rclcpp std_msgs sensor_msgs)

install(TARGETS hipnuc_imu_driver DESTINATION lib/${PROJECT_NAME})
install(DIRECTORY
  config launch
  DESTINATION share/${PROJECT_NAME}
)

ament_package()
