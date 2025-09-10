cmake_minimum_required(VERSION 3.24)
project(ModulacolorCore LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
  set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake" CACHE STRING "" FORCE)
endif()

find_package(glfw3 CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(fmt CONFIG REQUIRED)
find_package(spdlog CONFIG REQUIRED)

add_executable(modulacolor
  src/main.cpp
  src/gl_utils.hpp
  src/shader_chunks.hpp
  src/modules.hpp
)

target_compile_definitions(modulacolor PRIVATE IMGUI_IMPL_OPENGL_LOADER_GLAD)
target_include_directories(modulacolor PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src)

target_link_libraries(modulacolor
  PRIVATE
    glfw
    imgui::imgui
    glad::glad
    glm::glm
    fmt::fmt
    spdlog::spdlog
)
