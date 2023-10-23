cmake_minimum_required(VERSION 3.1)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(test-app)

file(GLOB SRCS *.cpp)
add_executable(${PROJECT_NAME} ${SRCS})
target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)
