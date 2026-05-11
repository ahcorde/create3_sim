cmake_minimum_required(VERSION 3.8)
project(irobot_create_ignition_plugins)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)

set(OpenGL_GL_PREFERENCE LEGACY)

# Find the Ignition gui library
find_package(gz-common5 QUIET)
find_package(gz-sim8 QUIET)
find_package(gz-plugin2 QUIET)

if(NOT gz-sim8_FOUND OR NOT gz-common5_FOUND OR NOT gz-plugin2_FOUND)
  message(WARNING "Ignition not found. Skipping ${PROJECT_NAME} package.")
  ament_package()
  return()
endif()

add_subdirectory(Create3Hmi)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
