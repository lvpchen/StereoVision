# Minimum required CMake version
cmake_minimum_required(VERSION 2.8)
 
# Project name
project(affine_transformation)
 
# Find the OpenCV installation
find_package(OpenCV REQUIRED)

# Find the Boost installation, specifically the components 'system' and 'filesystem'
find_package(Boost REQUIRED COMPONENTS system filesystem)

# ${PROJECT_SOURCE_DIR} is the name of the root directory of the project
# TO_NATIVE_PATH converts the path ${PROJECT_SOURCE_DIRS}/data/ to a full path and the file()
# command stores it in DATA_FOLDER
file(TO_NATIVE_PATH "${PROJECT_SOURCE_DIR}/data/" DATA_FOLDER)
# set case1 to DATA_FOLDER/CASE_1 - this is where we will put our templates for
# constructing the vocabulary
set(LEFT_FOLDER "${DATA_FOLDER}left/")
set(RIGHT_FOLDER "${DATA_FOLDER}right/")

# set the configuration input file to ${PROJECT_SOURCE_DIR}/Config.h.in and the includable header
# file holding configuration information to ${PROJECT_SOURCE_DIR}/include/Config.h
configure_file("${PROJECT_SOURCE_DIR}/Config.h.in" "${PROJECT_SOURCE_DIR}/include/Config.h")

# Other directories where header files for linked libraries can be found
include_directories(${OpenCV_INCLUDE_DIRS} "${PROJECT_SOURCE_DIR}/include" ${Boost_INCLUDE_DIRS})
 
# executable produced as a result of compilation
add_executable(out src/distance.cpp)

# libraries to be linked with this executable - OpenCV and Boost (system and filesystem components)
target_link_libraries(out ${OpenCV_LIBS} ${Boost_SYSTEM_LIBRARY} ${Boost_FILESYSTEM_LIBRARY})

