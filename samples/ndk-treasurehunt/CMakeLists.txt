cmake_minimum_required(VERSION 3.4.1)

project(treasurehunt_jni)

set(SOURCE src/main/jni/treasure_hunt_jni.cc
           src/main/jni/treasure_hunt_renderer.cc
           src/main/jni/treasure_hunt_renderer.h
           src/main/jni/world_layout_data.h)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

include_directories("src/main/jni")
include_directories(${GRADLE_PROJECT_ROOT}/libraries/headers)

add_library(gvr SHARED IMPORTED)
set_target_properties(gvr PROPERTIES IMPORTED_LOCATION
    ${GRADLE_PROJECT_ROOT}/libraries/jni/${ANDROID_ABI}/libgvr.so)

add_library(gvr_audio SHARED IMPORTED)
set_target_properties(gvr_audio PROPERTIES IMPORTED_LOCATION
    ${GRADLE_PROJECT_ROOT}/libraries/jni/${ANDROID_ABI}/libgvr_audio.so)

link_directories(${GRADLE_PROJECT_ROOT}/libraries/jni/${ANDROID_ABI})

add_library(treasurehunt_jni SHARED ${SOURCE})

target_link_libraries(treasurehunt_jni EGL android GLESv2 log
                                       gvr gvr_audio)


