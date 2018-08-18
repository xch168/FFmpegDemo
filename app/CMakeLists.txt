# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)


add_library( MyFFmpeg
             SHARED
             src/main/cpp/native-lib.cpp )


find_library( log-lib
              log )

find_library( android-lib
              android )

# 设置ffmpeg库所在路径的目录
set(distribution_DIR ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI})

add_library( avutil-56
        SHARED
        IMPORTED )
set_target_properties( avutil-56
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/libavutil-56.so)

add_library( swresample-3
        SHARED
        IMPORTED )
set_target_properties( swresample-3
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/libswresample-3.so)

add_library( avfilter-7
        SHARED
        IMPORTED )
set_target_properties( avfilter-7
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/libavfilter-7.so)

add_library( avformat-58
        SHARED
        IMPORTED )
set_target_properties( avformat-58
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/libavformat-58.so)

add_library( swscale-5
        SHARED
        IMPORTED )
set_target_properties( swscale-5
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/libswscale-5.so)


add_library( avcodec-58
        SHARED
        IMPORTED )
set_target_properties( avcodec-58
        PROPERTIES IMPORTED_LOCATION
        ${distribution_DIR}/libavcodec-58.so)

# 添加ffmpeg头文件路径
include_directories(src/main/jniLibs/include)


target_link_libraries( MyFFmpeg
        avcodec-58
        avfilter-7
        avformat-58
        avutil-56
        swresample-3
        swscale-5
        ${log-lib}
        ${android-lib} )