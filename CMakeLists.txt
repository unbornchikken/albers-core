cmake_minimum_required(VERSION 2.8)

# Name of the project (will be the name of the plugin)
project (addon)

# Essential include files to build a node addon,
# you should add this line in every CMake.js based project.
include_directories(${CMAKE_JS_INC})

# Declare the location of the source files
file(GLOB SOURCE_FILES "src/*.cc")

message(STATUS "SOURCE_FILES = ${SOURCE_FILES}")

# build dependency
# set up include-directories
include_directories(
  "${PROJECT_SOURCE_DIR}/deps/datamodel"
  )
add_subdirectory (deps)

# This line will tell CMake that we're building a shared library
# from the above source files
# named after the project's name
add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES})

# This line will give our library file a .node extension without any "lib" prefix
set_target_properties(${PROJECT_NAME} PROPERTIES PREFIX "" SUFFIX ".node")

# Essential library files to link to a node addon,
# you should add this line in every CMake.js based project.
target_link_libraries(${PROJECT_NAME} ${CMAKE_JS_LIB})

