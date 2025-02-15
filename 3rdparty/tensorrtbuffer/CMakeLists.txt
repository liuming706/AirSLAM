cmake_minimum_required(VERSION 3.6)
project(tensorrtbuffer)

set(CMAKE_CXX_STANDARD 17)
message("CMAKE_SOURCE_DIR: ${CMAKE_SOURCE_DIR}")

#set(TensorRT_ROOT "/home/ubt/workspace/3rdparty/release/TensorRT-8.6.1.6")# 修改该路径
#set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
set(TensorRT_ROOT "/home/ubt/workspace/3rdparty/release/TensorRT-8.6.1.6")
#include(${PROJECT_SOURCE_DIR}/cmake/FindTensorRT.cmake)
set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})
find_package(TensorRT REQUIRED)
message("TensorRT_LIBRARIES: ${TensorRT_LIBRARIES}")
message("TensorRT_INCLUDE_DIRS: ${TensorRT_INCLUDE_DIRS}")
message("TENSORRT_INCLUDE_DIRS: ${TENSORRT_INCLUDE_DIRS}")
if(POLICY CMP0146)
    cmake_policy(SET CMP0146 OLD)
endif()

find_package(CUDA REQUIRED)
include_directories("${CUDA_INCLUDE_DIRS}")

include_directories(
    ${PROJECT_SOURCE_DIR}/include
)

set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

add_library(tensorrtbuffer SHARED src/logger.cpp src/sample_options.cpp src/sample_utils.cpp)
target_include_directories(
  tensorrtbuffer PUBLIC 
         $<BUILD_INTERFACE:${TensorRT_INCLUDE_DIRS}>
         )





