cmake_minimum_required(VERSION 2.8.9)
if(NOT ITK_SOURCE_DIR)
  include(itk-module-init.cmake)
endif()
project(ITKVideoBridgeOpenCV)

set(ITKVideoBridgeOpenCV_LIBRARIES ITKVideoBridgeOpenCV)

set(ITKVideoBridgeOpenCV_SYSTEM_INCLUDE_DIRS ${OpenCV_INCLUDE_DIRS})
set(ITKVideoBridgeOpenCV_SYSTEM_LIBRARY_DIRS ${OpenCV_LIB_DIR})

if(NOT ITK_SOURCE_DIR)
 find_package(ITK REQUIRED)
 list(APPEND CMAKE_MODULE_PATH ${ITK_CMAKE_DIR})
 include(ITKModuleExternal)
else()
 itk_module_impl()
endif()
