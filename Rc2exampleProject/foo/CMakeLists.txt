cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions -fpermissive -frtti")

include_directories(
            ${ANDROID_NDK}/sources/android/cpufeatures
        )


add_library(foo
             SHARED
             ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/native-lib.cpp
         )

add_library(cpufeatures ${ANDROID_NDK}/sources/android/cpufeatures/cpu-features.c)

find_library( log-lib log)

target_link_libraries( # Specifies the target library.
                       foo

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib}
                       cpufeatures
                   )
