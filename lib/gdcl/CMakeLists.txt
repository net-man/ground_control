cmake_minimum_required(VERSION 3.11)

project(gdcl
  LANGUAGES CXX
)

message("configuring gdcl")

set (CMAKE_CXX_STANDARD 17)

include_directories(include)

include_directories(${PROJECT_SOURCE_DIR}/lib/lua)
include_directories(${PROJECT_SOURCE_DIR}/lib/sol2/include)

include_directories(${PROJECT_SOURCE_DIR}/lib/serialib)

include_directories(${PROJECT_SOURCE_DIR}/lib/libstem_gamepad/source)

# turn on all sol safeties. Although not all of them are required, at least use
# SOL_SAFE_NUMERICS to destinguish intagers and floating point numbers.
add_definitions(-DSOL_ALL_SAFETIES_ON)

add_library(gdcl
 include/gdcl/util.h
 include/gdcl/timer.h
 include/gdcl/net/net.h
 include/gdcl/net/packets.h
 include/gdcl/net/net_serial.h
 include/gdcl/net/net_nrf24l01.h
 include/gdcl/net/net_stream_writer.h
 include/gdcl/script.h
 include/gdcl/bot.h
 include/gdcl/input.h
 include/gdcl/gdcl.h
 src/gdcl/util.cpp
 src/gdcl/timer.cpp
 src/gdcl/net/net.cpp
 src/gdcl/net/net_serial.cpp
 src/gdcl/net/net_nrf24l01.cpp
 src/gdcl/net/net_stream_writer.cpp
 src/gdcl/script.cpp
 src/gdcl/bot.cpp
 src/gdcl/input.cpp
)

target_link_libraries(gdcl libstem_gamepad serialib lua_static sol2)