cmake_minimum_required(VERSION 2.8)
project(foo)
include_directories(/path/to/overlay/devel/include /opt/ros/indigo/include)
include_directories(SYSTEM /path/to/overlay/devel/include)
add_executable(foo foo.cpp)

# Yields:
# /usr/bin/c++    -isystem /path/to/overlay/devel/include     -I/opt/ros/indigo/include    -o CMakeFiles/foo.dir/foo.cpp.o -c /home/jbohren/scratch/isystem/foo.cpp
