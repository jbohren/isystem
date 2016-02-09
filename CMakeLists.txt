cmake_minimum_required(VERSION 2.8)
project(foo)
include_directories(/opt/ros/indigo/include)
include_directories(SYSTEM /opt/ros/indigo/include)
add_executable(foo foo.cpp)

# Yields:
# /usr/bin/c++    -isystem /opt/ros/indigo/include    -o CMakeFiles/foo.dir/foo.cpp.o -c /home/jbohren/scratch/isystem/foo.cpp
