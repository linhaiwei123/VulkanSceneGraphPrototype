VulkanSceneGraphPrototype (VSG) is a prototype for a modern scene graph library built upon Vulkan graphics/compute API.  The software is written in C++17, and follows the [CppCoreGuidlines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines).

## Prerequisites
* C++17 complient compiler i.e. g++ 7.3 or later, Clang 6.0 or later, Visual Studio S2017 or later.
* [Vulkan](https://vulkan.lunarg.com/) 1.1 or later.
* [CMake](https://www.cmake.org) 3.5 or later.
* [GLFW](https://www.glfw.org)  3.3 or later.  The plan is to implement native Windows so this dependency will
 later be removed.

The above dependency versions are known to work so they've been set as the current minimum, it may be possible to build against oldeer versions.  If you find success with older versions let us know and we can related the version info.

## Building the VSG

Command line instructions for default building of static library (.a/.lib) in source:

    git clone https://github.com/robertosfield/VulkanSceneGraphPrototype.git
    cd VulkanSceneGraphPrototype
    cmake .
    make -j 8
    make install

Command line instructions for building shared library (.so/.lib + .dll) in out of source:

    git clone https://github.com/robertosfield/VulkanSceneGraphPrototype.git
    mkdir vsg-sharead-build
    cd vsg-shared-build
    cmake ../VulkanSceneGraphPrototype -DBUILD_SHARED_LIBS=ON
    make -j 8
    make install

## Using the VSG within your own projects

The project is currently a prototype that is undergoing continuous revisions so it isn't recommend to use as base for long term software development, at this point it's available for developers who want to test the bleeding edge and provide feedback on it's fitness for purpose.

To assist with setting up software to work with the VSG we provided [FindVSG.cmake](https://github.com/robertosfield/VulkanSceneGraphPrototype/blob/master/CMakeModules/FindVSG.cmake), [FindGLFW.cmake](https://github.com/robertosfield/VulkanSceneGraphPrototype/blob/master/CMakeModules/FindGLFW.cmake) and [FindVulkan.cmake](https://github.com/robertosfield/VulkanSceneGraphPrototype/blob/master/CMakeModules/FindVulkan.cmake) within the [VullkanSceneGraphPrototype/CMakeModules](https://github.com/robertosfield/VulkanSceneGraphPrototype/tree/master/CMakeModules) directory.  Feel free to copy these into your own project.

Within your CMake CMakeLists.txt script to find the VSG related dependencies you'll need to add:

   find_package(VSG)
   find_package(GLFW)
   find_package(Vulkan)

To select C++17 compilation you'll need:

    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    set(CMAKE_CXX_EXTENSIONS OFF)

To link your lib/application to required dependnecies you'll need:

    target_link_libraries(mytargetname VSG::VSG GLFW::GLFW Vulkan::Vulkan)

This will tell CMAke to set up all the appropriate include paths, libs and any definitions (such as the VSG_SHARED_LIBRARY #define that is required under Windows with shared library builds to select the correct decltype()).

## Examples of VSG in testing/in use/how to work with VSG

It's still very early days for the project so we don't have many projects that link to the VSG to reference, for our own testing purposes we have two project which may serve as an assistance to how to compile against the VSG and how to use parts of it's API.  These projects are:
* [osg2vsg](https://github.com/robertosfield/osg2vsg)
* [vsgFramework](https://github.com/robertosfield/vsgFramework)


## General background documents used in dev process
* [Areas of Interest](docs/AreasOfInterest.md)
* [3rd Party Resources](docs/3rdPartyResources.md)
