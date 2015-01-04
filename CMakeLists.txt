cmake_minimum_required(VERSION 2.8)

project(guitarfusion)

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/CMakeModules")

set(DOCS_OUTPUT_DIR "${CMAKE_SOURCE_DIR}/build")
set(DOCS_TEMP_DIR "${CMAKE_SOURCE_DIR}/build/tmp")


add_subdirectory(src)

