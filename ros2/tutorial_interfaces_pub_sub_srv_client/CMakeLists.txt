cmake_minimum_required(VERSION 3.5)
project(tutorial_interfaces_pub_sub_srv_client)

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
find_package(tutorial_interfaces REQUIRED)

add_executable(pub src/pub.cpp)
ament_target_dependencies(pub rclcpp tutorial_interfaces)

add_executable(sub src/sub.cpp)
ament_target_dependencies(sub rclcpp tutorial_interfaces)

add_executable(server src/service.cpp)
ament_target_dependencies(server rclcpp tutorial_interfaces)

add_executable(client src/client.cpp)
ament_target_dependencies(client rclcpp tutorial_interfaces)

install(TARGETS 
      pub
      sub 
      server
      client
      DESTINATION lib/${PROJECT_NAME})

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
