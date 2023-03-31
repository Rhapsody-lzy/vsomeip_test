cmake_minimum_required  (VERSION 2.8.7)

project  (vSomeIPServiceExample)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -std=c++11")

find_package(Threads  REQUIRED)

include_directories("/home/lg/vsomeip")

link_directories("/usr/local/lib")

include_directories(${VSOMEIP_INCLUDE_DIRS})

include_directories(${Boost_INCLUDE_DIR})

find_package(vsomeip3 REQUIRED)

add_executable  (subscribe-sample ../subscribe-sample.cpp)

target_link_libraries(subscribe-sample vsomeip3 pthread)

add_executable  (notify-sample ../notify-sample.cpp)

target_link_libraries(notify-sample vsomeip3 pthread)
