cmake_minimum_required(VERSION 3.22)
project(FrogSpawner LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Vulkan REQUIRED)
add_subdirectory(third_party/glfw)

add_executable(FrogSpawner src/main.cpp src/vk_engine.cpp src/vk_engine.h src/vk_initialisers.cpp src/vk_initialisers.h src/VkBootstrap.cpp src/VkBootstrap.h third_party/imgui/imgui.cpp third_party/imgui/imgui.h third_party/imgui/backends/imgui_impl_glfw.cpp third_party/imgui/backends/imgui_impl_glfw.h third_party/imgui/backends/imgui_impl_vulkan.cpp third_party/imgui/backends/imgui_impl_vulkan.h third_party/imgui/imgui_draw.cpp third_party/imgui/imgui_tables.cpp third_party/imgui/imgui_widgets.cpp)


target_include_directories(FrogSpawner PRIVATE src ${Vulkan_INCLUDE_DIRS} third_party/glfw/include third_party/glm third_party/imgui third_party/imgui/backends)
target_link_libraries(FrogSpawner PRIVATE ${Vulkan_LIBRARIES} glfw)