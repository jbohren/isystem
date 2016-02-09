I ran into a problem recently where a package I was building set a SYSTEM include directory which was already a non-SYSTEM include directory imported from a dependency. When this happened, CMake dropped the non-SYSTEM directory in favor of the SYSTEM one, causing my build to fail.

Should this be the correct behavior? [According to GCC](https://gcc.gnu.org/onlinedocs/cpp/System-Headers.html), it gives precedence to non-SYSTEM include directories, and specifying both for the same path produces a warning.

> All directories named by -isystem are searched after all directories named by -I, no matter what their order was on the command line. If the same directory is named by both -I and -isystem, the -I option is ignored. GCC provides an informative message when this occurs if -v is used.

With CMake, if both are specified, it drops the non-SYSTEM include and fails silently. Should CMake be dropping one of the options at all?
