cmake_minimum_required(VERSION 3.5)

project(lcms2 VERSION 2.8 LANGUAGES C)

list(INSERT CMAKE_MODULE_PATH 0 "${PROJECT_SOURCE_DIR}/cmake")

# Install to a directory named installed, unless the install location was already set
# when calling CMake
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "${CMAKE_SOURCE_DIR}/installed" CACHE PATH "..." FORCE)
endif()

add_subdirectory(src)
