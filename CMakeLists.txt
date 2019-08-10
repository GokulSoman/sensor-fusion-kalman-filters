cmake_minimum_required(VERSION 3.14)
project(sensor_fusion_kalman_filters)

set(CMAKE_CXX_STANDARD 14)

add_executable(sensor_fusion_kalman_filters kalman_filter.cpp kalman_filter.h main.cpp tracking.cpp tracking.h measurement_package.h)