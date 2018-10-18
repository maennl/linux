cmake_minimum_required(VERSION 3.12)
project(nanopi_neo_plus2)

set(CMAKE_CXX_STANDARD 14)

SET(KERNEL_SOURCES "${CMAKE_CURRENT_LIST_DIR}")

set(ARCH_TARGET arm64)
set(COMPILER aarch64-linux-gnu-)

Set(image_cmd make Image dtbs ARCH=${ARCH_TARGET} CROSS_COMPILE=${COMPILER} )

add_custom_command(
        OUTPUT IMAGE
        COMMAND make ARGS Image dtbs ARCH=${ARCH_TARGET} CROSS_COMPILE=${COMPILER}
        WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
        VERBATIM  USES_TERMINAL
)

ADD_CUSTOM_TARGET(Image ALL DEPENDS IMAGE)

include_directories(${KERNEL_SOURCES}/include)
