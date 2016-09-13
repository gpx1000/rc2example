cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions -fno-strict-aliasing")

include_directories(
            include
        )


add_library( foo4
             STATIC
             ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/native-lib.cpp
         )

find_library( log-lib log)

target_link_libraries( # Specifies the target library.
                       foo4

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib}
                   )
