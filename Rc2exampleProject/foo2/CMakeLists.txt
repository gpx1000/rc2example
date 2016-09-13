cmake_minimum_required(VERSION 3.4.1)

set(EXTERNAL_PATH ../../../External/)

include_directories(
            ${EXTERNAL_PATH}
        )


add_library( foo2
             STATIC
             ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/native-lib.cpp
         )

find_library( z-lib z )

target_link_libraries( # Specifies the target library.
                       foo2

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib}
                   )
