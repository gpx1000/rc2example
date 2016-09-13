cmake_minimum_required(VERSION 3.4.1)

set(TOP_PATH ../../..)
set(EXTERNAL_PATH ${TOP_PATH}/External/)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions -fpermissive")

include_directories(
		${EXTERNAL_PATH}include
        )


add_library( bar3
             SHARED
            ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/native-lib.cpp
         )

target_link_libraries(
                       bar3
                   )

