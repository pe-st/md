# CLion

## CMake

### CMake Options

can be set on the command line (`-D<option>=<value>`) or in CMakeLists.txt (`set(<option> <value>)`)

- `-DCMAKE_VERBOSE_MAKEFILE=ON` show the

### CMake Options in CLion

- CMake Generation Path: bin\cmake-build-debug

## Inspections

Use my IDE profile `C++03` instead of the default one for pre-2011 code

## Clang-Tidy

- [Announcement for CLion 2017.2 EAP](https://blog.jetbrains.com/clion/2017/04/clion-2017-2-eap-clang-tidy/)
- [CLion default configuration](https://confluence.jetbrains.com/display/CLION/Clang-Tidy+in+CLion%3A+default+configuration)
- [List of checks](https://clang.llvm.org/extra/clang-tidy/checks/list.html)

### List of checks to remove for C++03

- boost-use-to-string
- modernize-use-*


