cmake_minimum_required(VERSION 3.5)
project(G2O_learn)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
list( APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/g2o/cmake_modules )

find_package(OpenCV REQUIRED)
find_package(Cholmod REQUIRED)
add_subdirectory(g2o)

SET(G2O_LIBS
        core
        types_slam3d
        solver_csparse
        stuff
        csparse_extension
        types_sba
        )

include_directories(${OpenCV_INCLUDE_DIRS} ${PROJECT_SOURCE_DIR}/g2o ${PROJECT_BINARY_DIR}/g2o "/usr/include/eigen3"
        ${CHOLMOD_INCLUDE_DIR})

set(SOURCE_FILES main.cpp)
add_executable(main ${SOURCE_FILES})
target_link_libraries(main ${OpenCV_LIBS} ${CHOLMOD_LIBRARIES} ${G2O_LIBS} )