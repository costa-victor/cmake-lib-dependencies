cmake_minimum_required(VERSION 3.20)

project(app VERSION 0.1.0)

# Set the project workspace, it's used as a reference for the installed files
set(PROJECT_WORKSPACE
    "${CMAKE_CURRENT_SOURCE_DIR}/../.."
    CACHE PATH "Project workspace"
)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

## headerOnlyLib info
set(headerOnlyLib_NAME   libShape)
set(headerOnlyLib_VERSION   0.5.0)
list(APPEND CMAKE_PREFIX_PATH "${PROJECT_WORKSPACE}/.project_libraries/cmake/${headerOnlyLib_NAME}-${headerOnlyLib_VERSION}")
find_package(${headerOnlyLib_NAME} ${headerOnlyLib_VERSION} CONFIG REQUIRED)

add_executable(${PROJECT_NAME})

target_sources(${PROJECT_NAME}
    PRIVATE
        src/main.cpp
)

target_include_directories(${PROJECT_NAME}
    PRIVATE
        src
)


target_link_libraries(${PROJECT_NAME} PRIVATE libShape::libShape)
