cmake_minimum_required(VERSION 3.22)
project(FrogSpawner LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SDL3_DIR "${CMAKE_CURRENT_SOURCE_DIR}/third_party/sdl3/cmake")
list(APPEND CMAKE_MODULE_PATH "${SDL3_DIR}")

find_package(Vulkan REQUIRED)
find_package(SDL3 REQUIRED CONFIG)

add_executable(FrogSpawner 
    src/main.cpp 
    src/vk_engine.cpp 
    src/vk_engine.h 
    src/vk_initialisers.cpp 
    src/vk_initialisers.h 
    third_party/imgui/imgui.h 
    third_party/imgui/imgui.cpp 
    third_party/imgui/imgui_demo.cpp 
    third_party/imgui/backends/imgui_impl_vulkan.cpp 
    third_party/imgui/backends/imgui_impl_vulkan.h 
    third_party/imgui/imgui_draw.cpp 
    third_party/imgui/imgui_tables.cpp 
    third_party/imgui/imgui_widgets.cpp
)

target_include_directories(FrogSpawner PRIVATE 
    ${CMAKE_CURRENT_SOURCE_DIR}/src 
    ${Vulkan_INCLUDE_DIRS} 
    ${CMAKE_CURRENT_SOURCE_DIR}/third_party/glm 
    ${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui 
    ${CMAKE_CURRENT_SOURCE_DIR}/third_party/imgui/backends
)

target_link_libraries(FrogSpawner PRIVATE 
    Vulkan::Vulkan 
    SDL3::SDL3
)

add_custom_command(TARGET FrogSpawner POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    "$<TARGET_FILE:SDL3::SDL3>"
    "$<TARGET_FILE_DIR:FrogSpawner>"
)