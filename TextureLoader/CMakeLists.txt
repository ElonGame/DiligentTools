cmake_minimum_required (VERSION 3.6)

project(TextureLoader CXX)

set(INCLUDE 
    include/DDSLoader.h
    include/dxgiformat.h
    include/pch.h
)

set(INTERFACE
    interface/Image.h
    interface/TextureLoader.h
    interface/TextureUtilities.h
)

set(SOURCE 
    src/DDSLoader.cpp
    src/Image.cpp
    src/TextureLoader.cpp
    src/TextureUtilities.cpp
)

add_library(TextureLoader STATIC ${SOURCE} ${INCLUDE} ${INTERFACE})
set_common_target_properties(TextureLoader)

target_include_directories(TextureLoader
PUBLIC
    interface
PRIVATE
    include
)

source_group("source" FILES ${SOURCE})
source_group("include" FILES ${INCLUDE})
source_group("interface" FILES ${INTERFACE})

target_link_libraries(TextureLoader 
PRIVATE 
    BuildSettings 
    Common 
    PlatformInterface 
    GraphicsEngineInterface 
    GraphicsAccessories
    LibJpeg 
    LibPng 
    LibTiff 
    ZLib
)

set_target_properties(TextureLoader PROPERTIES
    FOLDER Tools
)