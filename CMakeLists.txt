cmake_minimum_required(VERSION 2.8)
project(VoxelRenderer)

subdirs(src include shader)

find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(GLUT REQUIRED)

set(SOURCES src/main.cpp src/noise.cpp)
set(HEADERS include/main.hpp include/noise.hpp)
set(SHADERS shader/textures.c)

if(CMAKE_COMPILER_IS_GNUCXX)
    message(STATUS "GCC detected, adding compile flags")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pedantic -Wall -Wextra")
    set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

# Put the GLM folder in the project in windows
elseif(MSVC)
    include_directories(${PROJECT_SOURCE_DIR}/glm)
endif()

add_executable(main ${SOURCES} ${HEADERS} ${SHADERS})
target_link_libraries(main ${OPENGL_LIBRARIES} ${GLEW_LIBRARIES} ${GLUT_LIBRARY})
