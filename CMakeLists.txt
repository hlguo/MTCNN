cmake_minimum_required(VERSION 2.8)

project(MTCNN)
set(CMAKE_CXX_STANDARD 11)

find_package(OpenCV 3.4 REQUIRED)

find_package(Caffe)
if(Caffe_LIBRARIES)
	include_directories(${Caffe_INCLUDE_DIRS})
	add_subdirectory(cpp)
else()
	message("Caffe not found, cpp was not built")
endif()

find_package(ncnn)
if(ncnn_FOUND)
	add_subdirectory(ncnn)
else()
	message("ncnn not found, ntcnn was not built")
endif()

#default build light, only depend on openblas
add_subdirectory(MTCNN-light)

#need opencv version >= 3.4.* or recompile opencv with conrtib module
add_subdirectory(Fast-MTCNN)