I ran into a problem recently where a package I was building set a SYSTEM include directory which was already a non-SYSTEM include directory imported from a dependency. When this happened, CMake dropped the non-SYSTEM directory in favor of the SYSTEM one, causing my build to fail.

Should this be the correct behavior? [According to GCC](https://gcc.gnu.org/onlinedocs/cpp/System-Headers.html), it gives precedence to non-SYSTEM include directories, and specifying both for the same path produces a warning.

> All directories named by -isystem are searched after all directories named by -I, no matter what their order was on the command line. If the same directory is named by both -I and -isystem, the -I option is ignored. GCC provides an informative message when this occurs if -v is used.

With CMake, if both are specified, it drops the non-SYSTEM include and fails silently. Should CMake be dropping one of the options at all?

For example, when building this project with any recent version of CMake on Linux, the build command is:

```bash
/usr/bin/c++  -isystem /path/to/overlay/devel/include  -I/opt/ros/indigo/include  -o CMakeFiles/foo.dir/foo.cpp.o -c /home/jbohren/scratch/isystem/foo.cpp
```

But with the three `incude_directory` options given in `CMakeLists.txt`, I would expect it to read:

```bash
/usr/bin/c++  -I/path/to/overlay/devel/include  -I/opt/ros/indigo/include  -isystem /path/to/overlay/devel/include  -o CMakeFiles/foo.dir/foo.cpp.o -c /home/jbohren/scratch/isystem/foo.cpp
```
