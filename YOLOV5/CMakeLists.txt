cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(example-app)
set(CMAKE_C_COMPILER clang)
set(CMAKE_CXX_COMPILER clang++)
find_package(OpenCV REQUIRED)
if (OpenCV_FOUND)
    # If the package has been found, several variables will
    # be set, you can find the full list with descriptions
    # in the OpenCVConfig.cmake file.
    # Print some message showing some of them
    message(STATUS "OpenCV library status:")
    message(STATUS "    version: ${OpenCV_VERSION}")
    message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}" \n)
else ()
    message(FATAL_ERROR "Could not locate OpenCV" \n)
endif()
find_package(Torch REQUIRED)
if (Torch_FOUND)
	message(STATUS "include path: ${Torch_INCLUDE_DIRS}"\n)
endif()
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${TORCH_CXX_FLAGS}")
add_executable(example-app example-app.cpp)
include_directories(
${PROJECT_SOURCE_DIR}/include
${OpenCV_INCLUDE_DIRS}
)

target_link_libraries(example-app "${OpenCV_LIBS}" "${TORCH_LIBRARIES}")
set_property(TARGET example-app PROPERTY CXX_STANDARD 14)
