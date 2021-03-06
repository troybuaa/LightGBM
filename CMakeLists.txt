cmake_minimum_required(VERSION 2.8)

PROJECT(lightgbm)

OPTION(USE_MPI "MPI based parallel learning" OFF)

if(USE_MPI)
  find_package(MPI REQUIRED)
  ADD_DEFINITIONS(-DUSE_MPI)
  MESSAGE(${MPI_LIBRARIES})
  MESSAGE(${MPI_CXX_LIBRARIES})
else()
  ADD_DEFINITIONS(-DUSE_SOCKET)
endif()

if(UNIX)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -fopenmp  -pthread -O2 -std=c++11")
endif()

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -fopenmp -O2 -std=c++11")

SET(LightGBM_HEADER_DIR ${PROJECT_SOURCE_DIR}/include)
SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR})
SET(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR})

ADD_SUBDIRECTORY(src)

