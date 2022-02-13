project(vkModelViewer)
cmake_minimum_required(VERSION 3.22)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_BUILD_TYPE DEBUG)
set(CMAKE_CXX_STANDARD 17)

# file(GLOB IMGUI_SRC "include/imgui/*.cpp" "include/imgui/*.h") # Adds all imgui related files into
                                                               # the application

if(WIN32)
        # Get rid of annoying MSVC warnings.
        add_definitions(-D_CRT_SECURE_NO_WARNINGS)

        # set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /d2cgsummary") # set(CMAKE_CXX_FLAGS
        # "${CMAKE_CXX_FLAGS} /Bt") # time spent in frontend (c1xx.dll) vs backend (c2.dll)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4") # Enable warning level 4
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP") # MultiProcessor compilation
        # Use solution folders for VS
        set_property(GLOBAL PROPERTY USE_FOLDERS ON)
endif(WIN32)

add_executable(vkModelViewer main.cpp)
target_sources(vkModelViewer PRIVATE main.cpp)
# target_link_libraries(vkModelViewer Vulkan)

# Vulkan
# set(Vulkan_LIBRARY "C:\\VulkanSDK\\1.2.198.1\\Lib\\vulkan-1.lib")
# set(Vulkan_INCLUDE_DIR "C:\\VulkanSDK\\1.2.198.1\\Include\\")
# find_package(Vulkan REQUIRED FATAL_ERROR)

find_package(Vulkan REQUIRED)
include_directories(${Vulkan_INCLUDE_DIRS})
target_link_libraries(vkModelViewer PRIVATE ${Vulkan_LIBRARIES})
