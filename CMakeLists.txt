cmake_minimum_required(VERSION 3.22)
project(OpenGLTutorial)
set(CMAKE_CXX_STANDARD 20)

include(FetchContent)
set(FETCHCONTENT_QUIET FALSE)

##########################################################################################
# GLFW
##########################################################################################

FetchContent_Declare(
    glfw
    GIT_REPOSITORY "https://github.com/glfw/glfw.git"
    GIT_TAG        "3.3.8"
    GIT_SHALLOW    TRUE
    GIT_PROGRESS   TRUE
)
FetchContent_MakeAvailable(glfw)

##########################################################################################
# GLAD
##########################################################################################

FetchContent_Declare(
    glad
    GIT_REPOSITORY "https://github.com/Dav1dde/glad"
    GIT_TAG        "v2.0.6"
    GIT_SHALLOW    TRUE
    GIT_PROGRESS   TRUE
)

FetchContent_GetProperties(glad)
if(NOT glad_POPULATED)
    message("Fetching glad")
    FetchContent_MakeAvailable(glad)

    add_subdirectory("${glad_SOURCE_DIR}/cmake" glad_cmake)
    glad_add_library(glad REPRODUCIBLE EXCLUDE_FROM_ALL LOADER API gl:core=4.6 EXTENSIONS GL_ARB_bindless_texture GL_EXT_texture_compression_s3tc)
endif()

##########################################################################################
# GLM Math Library
##########################################################################################

FetchContent_Declare(
    glm
    GIT_REPOSITORY "https://github.com/g-truc/glm.git"
    GIT_TAG        "1.0.1"
    GIT_SHALLOW    TRUE
    GIT_PROGRESS   TRUE
)
FetchContent_MakeAvailable(glm)

##########################################################################################
# Project executable setup
##########################################################################################

add_executable(
    OpenGLTutorial
    src/main.cpp
)

target_link_libraries(OpenGLTutorial PUBLIC 
    glfw
    glad
    glm::glm
)
