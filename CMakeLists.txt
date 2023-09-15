include(FetchContent)
cmake_minimum_required(VERSION 3.25)
set(CMAKE_CXX_COMPILER clang++)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)
set(BUILD_SHARED_LIBS OFF)

project(main
  LANGUAGES CXX
  VERSION 1.0.1
  DESCRIPTION "Dear ImGUI app"
  HOMEPAGE_URL "https://pouyacode.net")

set(OpenGL_GL_PREFERENCE "LEGACY")
find_package(OpenGL 3 REQUIRED)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

FetchContent_Declare(glfw
  URL https://github.com/glfw/glfw/archive/refs/tags/3.3.8.tar.gz
  URL_HASH MD5=55d99dc968f4cec01a412562a7cf851c)

FetchContent_MakeAvailable(glfw)

FetchContent_Declare(imgui
  URL https://github.com/ocornut/imgui/archive/refs/tags/v1.89.9-docking.tar.gz
  URL_HASH MD5=5530891015d1966067827bd1c25f51c2)

FetchContent_MakeAvailable(imgui)

add_library(imgui STATIC
  ${imgui_SOURCE_DIR}/imgui.cpp
  ${imgui_SOURCE_DIR}/imgui_draw.cpp
  ${imgui_SOURCE_DIR}/imgui_demo.cpp
  ${imgui_SOURCE_DIR}/imgui_tables.cpp
  ${imgui_SOURCE_DIR}/imgui_widgets.cpp

  ${imgui_SOURCE_DIR}/backends/imgui_impl_glfw.cpp
  ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp)

target_link_libraries(imgui PRIVATE glfw OpenGL::GL)
target_compile_definitions(imgui PRIVATE IMGUI_IMPL_OPENGL_LOADER)

target_include_directories(imgui PUBLIC ${imgui_SOURCE_DIR} ${imgui_SOURCE_DIR}/backends)

add_executable(main main.cpp)
target_link_libraries(main imgui)
