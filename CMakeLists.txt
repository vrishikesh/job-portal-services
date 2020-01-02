cmake_minimum_required(VERSION 3.0)

project(micro-service)

# Configure required libraries
find_library(CPPREST_LIB cpprest)
find_package(Boost REQUIRED COMPONENTS random system thread filesystem chrono atomic date_time regex log program_options)
find_package(Threads REQUIRED)
find_package(OpenSSL 1.0.1 REQUIRED)
set(OPENSSL_VERSION "1.0.1")

# Configure compiler options
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11 -DBOOST_LOG_DYN_LINK")

# Project construction
set(EXECUTABLE_OUTPUT_PATH ./${CMAKE_BUILD_TYPE})
set(CMAKE_CXX_STANDARD 11)

# source files
file(
    GLOB_RECURSE
    MY_SOURCE_FILES
    src/*
)
#set(SOURCE src/main.cpp)
add_executable(${PROJECT_NAME} ${MY_SOURCE_FILES})

# headers search paths
set(MICROSERVICE_INCLUDE_DIR "./src/foundation/include")
set(HEADER_SEARCH_PATHS ${MICROSERVICE_INCLUDE_DIR})

include_directories(${HEADER_SEARCH_PATHS})

target_link_libraries(${PROJECT_NAME}
    ${CPPREST_LIB}
    Boost::boost
    Boost::random
    Boost::system
    Boost::thread
    Boost::filesystem
    Boost::chrono
    Boost::atomic
    Boost::date_time
    Boost::regex
    OpenSSL::SSL)