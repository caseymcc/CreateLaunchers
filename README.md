[![hunter](https://img.shields.io/badge/hunter-CreateLaunchers-blue.svg)](https://github.com/ruslo/hunter)

# CreateLaunchers
CMake module for creating batch/shell scripts and Visual Studio user file for launching your application.

This is a modified version of the CreateLaunchers from https://github.com/rpavlik/cmake-modules. It has been seperated from the rest of the cmake modules into its own repo and provided with cmake installer and setup as a hunter package.

Usage
-----

```cmake

  #use hunter to get the latest version
  #optional, you can just download and include it in you CMakeLists file
  hunter_add_package(CreateLauncher)
  find_package(CreateLauncher CONFIG REQUIRED)

  #Now include the modules, directory for CreateLaunchers would
  # have been add to CMAKE_MODULE_PATH
  include(CreateLaunchers)

  #Creates bash or shell script to launch the target from commandline
  # -When using a VS generator it also creates VS .user so that the
  #   target can be launched by the VS debugger with the requested settings
  # -When using gdb it will create shell scripts that will call gdb to start
  #   the target with the requested settings
  create_target_launcher(<targetname>
    [COMMAND <target command>]
    [ARGS <args...>]
    [FORWARD_ARGS]
    [RUNTIME_LIBRARY_DIRS <dir...>]
    [WORKING_DIRECTORY <dir>]
    [ENVIRONMENT <VAR=value> [<VAR=value>...]])
```

CreateLaunchers uses file(GENERATE ...) internally to create the launchers therefore it will support generator expressions.
