cmake_minimum_required(VERSION 3.10)

project(HelloWorld)

# 指定为C++11 版本
set(CMAKE_CXX_STANDARD 11)

add_executable(ws cmd/ws.cpp)
add_executable(apiserver cmd/apiserver.cpp)

# fmt
find_package(fmt CONFIG REQUIRED)
target_link_libraries(ws PRIVATE fmt::fmt)

# websocketpp
find_package(websocketpp CONFIG REQUIRED)
target_link_libraries(ws PRIVATE websocketpp::websocketpp)

# Crow
find_package(Crow CONFIG REQUIRED)
target_link_libraries(apiserver PUBLIC Crow::Crow)

