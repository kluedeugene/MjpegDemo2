cmake_minimum_required(VERSION 3.12)
project(H264Demo)
 
set(CMAKE_CXX_STANDARD 11)
 
if (CMAKE_BUILD_TYPE STREQUAL "")
    message(STATUS "CMAKE_BUILD_TYPE not defined, 'Release' will be used")
    set(CMAKE_BUILD_TYPE "Release")
endif()
 
 
find_package( OpenMP REQUIRED)
if(OPENMP_FOUND)
    message("OPENMP FOUND")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
endif()
 
set(OpenCV_DIR "C:/opencv/build")
find_package(OpenCV REQUIRED)
if(OpenCV_FOUND)
    message(STATUS "OPENCV found")
else (OpenCV_FOUND)
    message(WARNING "OPENCV is disabled or not found")
    return()
endif()
 

add_executable(H264EncoderDemo H264EncoderDemo.cpp h264decoder.cpp h264encoder.cpp)
target_link_libraries(H264EncoderDemo ${OpenCV_LIBRARIES}
        avformat avdevice  avcodec avutil  avfilter postproc  swresample swscale)