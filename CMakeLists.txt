cmake_minimum_required (VERSION 3.8)
project(Rasterizer VERSION 1.0)
set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT Rasterizer)
project(Raytracer VERSION 1.0)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DDEBUG")

find_package(SDL2 REQUIRED PATHS ${PROJECT_SOURCE_DIR}/library_binaries)
include_directories(${PROJECT_SOURCE_DIR}/library_binaries/include/SDL2)

file(GLOB_RECURSE RASTERIZER_SOURCE "Rasterizer/*.*")
file(GLOB_RECURSE RAYTRACER_SOURCE "Raytracer/*.*")

file(GLOB LIBRARIES "library_binaries/bin/*.dll")
file(COPY ${LIBRARIES} DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/build/Release)
file(COPY ${LIBRARIES} DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/build/Debug)
file(COPY ${LIBRARIES} DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/build/MinSizeRel)
file(COPY ${LIBRARIES} DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/build/RelWithDebInfo)

add_executable(Rasterizer ${RASTERIZER_SOURCE})
add_executable(Raytracer ${RAYTRACER_SOURCE})

target_link_libraries(Rasterizer ${SDL2_LIBRARIES})
target_link_libraries(Raytracer ${SDL2_LIBRARIES})