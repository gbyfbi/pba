CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
# FindCUDA required cmake version 2.8

# Author : Pierre Moulon pmoulon@gmail.com
# http://imagine.enpc.fr/~moulonp/
# Date : May 2011.
# README :

PROJECT(PBA)

#Searching CUDA
FIND_PACKAGE(CUDA)
if (CUDA_FOUND) 
  MESSAGE("CUDA FOUND")
  SET(CUDA_NVCC_FLAGS "${CUDA_NVCC_FLAGS} --generate-code arch=compute_52,code=sm_52 --generate-code arch=compute_35,code=sm_35")
else (CUDA_FOUND)
  MESSAGE("CUDA NOT FOUND. Cuda MCBA will not be compiled")
endif (CUDA_FOUND)

IF(CMAKE_COMPILER_IS_GNUCXX)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC -O2 -g -Wall -Wno-deprecated -pthread")
  #Setup here your compilation flags depending of your platform
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=native -mfpmath=sse -fpermissive")
  #SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -march=core2 -mfpmath=sse")
ENDIF(CMAKE_COMPILER_IS_GNUCXX)

include_directories(.
                    ./src/pba)
ADD_SUBDIRECTORY(src)
