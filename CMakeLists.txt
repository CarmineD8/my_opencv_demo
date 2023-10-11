cmake_minimum_required(VERSION 3.5)
project(my_opencv_demo)

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
find_package(cv_bridge REQUIRED)
find_package(image_transport REQUIRED)
find_package(OpenCV REQUIRED)

add_executable(opencv_ros2_node src/opencv_ros2_node.cpp)
ament_target_dependencies(opencv_ros2_node rclcpp std_msgs sensor_msgs cv_bridge image_transport OpenCV)

add_executable(image_transport_node src/image_transport_demo.cpp)
ament_target_dependencies(image_transport_node rclcpp std_msgs sensor_msgs cv_bridge image_transport OpenCV)

add_executable(opencv_ros2_subscriber src/opencv_ros2_subscriber.cpp)
ament_target_dependencies(opencv_ros2_subscriber rclcpp std_msgs sensor_msgs cv_bridge image_transport OpenCV)

install(TARGETS
   opencv_ros2_node image_transport_node opencv_ros2_subscriber
   DESTINATION lib/${PROJECT_NAME}
 )


if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
