cmake_minimum_required(VERSION 3.4.1)

add_library(bbhelper SHARED c++/directBufferAndroid.cpp)

target_compile_options(bbhelper PRIVATE -DBUILD_FOR_ANDROID)

# הוספת תמיכה ב-16KB page size
if(ANDROID_16KB_PAGE_SIZE)
    target_compile_options(bbhelper PRIVATE -DANDROID_16KB_PAGE_SIZE=1)
    set_target_properties(bbhelper PROPERTIES
        LINK_FLAGS "-Wl,-z,common-page-size=16384 -Wl,-z,max-page-size=16384"
    )
endif()
