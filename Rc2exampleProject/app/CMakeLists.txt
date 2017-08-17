cmake_minimum_required(VERSION 3.4.1)

option(BUILD_OCULUS "build oculus" OFF)

STRING(REGEX REPLACE "\\\\" "/" TOP_PATH ${TOP_PATH})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions")

set(libjit_SOURCES )

set(libjit_INCLUDE_DIRS
    ${TOP_PATH}/include
)


if(BUILD_OCULUS)
    list(APPEND libjit_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/native-lib.cpp
        )
else(BUILD_OCULUS)
    list(APPEND libjit_SOURCES
            ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp/native-lib.cpp
            )
endif(BUILD_OCULUS)

include_directories (
    ${libjit_INCLUDE_DIRS}
)

add_library(
             native-lib
             SHARED
             ${libjit_SOURCES}
         )

add_library(foo SHARED IMPORTED)
set_target_properties(
            foo
            PROPERTIES
            IMPORTED_LOCATION
            ${TOP_PATH}/Rc2exampleProject/foo/build/intermediates/cmake/release/obj/armeabi-v7a/libfoo.so
        )

add_library( bar2 STATIC IMPORTED )
set_target_properties(
            bar2
            PROPERTIES
            IMPORTED_LOCATION
            ${TOP_PATH}/Rc2exampleProject/bar2/.externalNativeBuild/cmake/release/armeabi-v7a/libbar2.a
        )

add_library( foo3 SHARED IMPORTED )
set_target_properties(
            foo3
            PROPERTIES
            IMPORTED_LOCATION
            ${TOP_PATH}/Rc2exampleProject/foo3/build/intermediates/binaries/release/obj/armeabi-v7a/libfoo3.so
        )

add_library(cpufeatures ${ANDROID_NDK}/sources/android/cpufeatures/cpu-features.c)

find_library( log-lib log )
find_library( EGL-lib EGL )
find_library( GLESv3-lib GLESv3 )
find_library( android-log android )
if(NOT BUILD_OCULUS)
    add_library( foo2 SHARED IMPORTED )
    set_target_properties(
                native-lib
                PROPERTIES
                IMPORTED_LOCATION
                ${TOP_PATH}/Rc2exampleProject/foo2/build/intermediates/cmake/release/obj/armeabi-v7a/libfoo2.so
            )

    target_link_libraries( native-lib ${log-lib} ${EGL-lib} ${GLESv3-lib} ${android-log} cpufeatures
                          "-Wl,--whole-archive" bar2 "-Wl,--no-whole-archive"
                          foo foo3 foo2
                          )
else(NOT BUILD_OCULUS)
    find_library( OpenSLES opensles)
    target_link_libraries( native-lib ${log-lib} ${EGL-lib} ${GLESv3-lib} ${android-log} cpufeatures
                          "-Wl,--whole-archive" bar2 "-Wl,--no-whole-archive"
                          foo bar3
                          )
endif(NOT BUILD_OCULUS)