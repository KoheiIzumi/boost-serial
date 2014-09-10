cmake_minimum_required(VERSION 2.8)

project(serial_async)

set(ENV{Boost_DIR})

if(WIN32)
set(Boost_ADDITIONAL_VERSIONS "1.54" "1.54.0")
endif(WIN32)

if(UNIX)
set(Boost_ADDITIONAL_VERSIONS "1.49" "1.49.0")
endif(UNIX)

set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)

if(WIN32)
find_package(Boost 1.54.0 COMPONENTS system thread filesystem)
endif(WIN32)

if(UNIX)
find_package(Boost 1.49.0 COMPONENTS system thread filesystem)
endif(UNIX)

add_definitions(${Boost_LIB_DIAGNOSTIC_DEFINITIONS})


include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}
	${Boost_INCLUDE_DIRS}
	${Boost_INCLUDE_DIR}
)

link_directories(
	${Boost_LIBRARY_DIRS}
	${Boost_LIBRARY_DIR}
)

set(SERIAL_SRCS
serial_async.cpp
)

add_executable(serial
	${SERIAL_SRCS}
)

target_link_libraries(serial
	${Boost_LIBRARIES}
)
