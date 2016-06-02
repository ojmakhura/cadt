cmake_minimum_required (VERSION 2.6)
project (cadt C)
set(CMAKE_BUILD_TYPE Release)

# ---[ Includes
set(CADT_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include)
include_directories(${CADT_INCLUDE_DIR})

set(CADT_SRC_DIR ${PROJECT_SOURCE_DIR}/source)
set(CADT_SAMPLE_DIR ${PROJECT_SOURCE_DIR}/examples)

# get all files recursively
file(GLOB_RECURSE SRC_FILES ${CADT_SRC_DIR}/*.c)
file(GLOB_RECURSE INCLUDE_FILES ${CADT_INCLUDE_DIR}/*.h)

# ---[ HDBSCAN version
set(CADT_TARGET_VERSION "1.0")
set(CADT_TARGET_SOVERSION "1.0")
add_definitions(-DCADT_VERSION=${CADT_TARGET_VERSION})

option(BUILD_TEST "Build samples" ON)

if (BUILD_TEST)
	add_subdirectory(${CADT_SAMPLE_DIR})
	set (EXTRA_LIBS ${EXTRA_LIBS} cadt)
endif (BUILD_TEST)

# -- project options
#set( CMAKE_C_FLAGS "-O0 -g3 -Wall -fmessage-length=0 ")

add_library(cadt SHARED ${SRC_FILES})
target_link_libraries(cadt m)
 
install (TARGETS cadt DESTINATION lib)
install (FILES ${INCLUDE_FILES} DESTINATION include)
