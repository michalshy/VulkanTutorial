cmake_minimum_required(VERSION 3.27)
project(HelloVulkan)

set(CMAKE_CXX_STANDARD 17)

set(GLFW_DIR "glfw-3.4.bin.WIN64") # This is where the downloaded glfw folder is located
set(GLFW_INCLUDE_DIR ${GLFW_DIR}/include) # The directory where GLFW header files are located
set(GLFW_LIB_DIR ${GLFW_DIR}/lib-mingw-w64) # The directory the LINKER will look for GLFW library. You'd want to change this depending on the compiler you're using.

# Make sure that Vulkan is installed properly
find_package(Vulkan REQUIRED)

message(STATUS "Vulkan_INCLUDE_DIR:= ${Vulkan_INCLUDE_DIR}")
message(STATUS "Vulkan_LIBRARY:= ${Vulkan_LIBRARY}")
message(STATUS "Vulkan_LIBRARIES:= ${Vulkan_LIBRARIES}")

add_executable(${PROJECT_NAME} main.cpp)

target_include_directories(${PROJECT_NAME}
        PRIVATE ${GLFW_DIR}/include
        ${Vulkan_INCLUDE_DIR}
)

target_link_directories(${PROJECT_NAME} PRIVATE ${GLFW_LIB_DIR})

target_link_libraries(${PROJECT_NAME}
        PRIVATE glfw3
        PRIVATE ${Vulkan_LIBRARIES}
)
