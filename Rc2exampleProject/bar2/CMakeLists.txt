cmake_minimum_required(VERSION 3.4.1)

set(TOP_PATH ../../..)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions -fpermissive")

include_directories(
            ${TOP_PATH}/include
        )


add_library( bar2
             STATIC
             ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/native-lib.cpp
         )

 add_library(cpufeatures ${ANDROID_NDK}/sources/android/cpufeatures/cpu-features.c)

target_link_libraries(
                       bar2
                       cpufeatures
                   )
