cmake_minimum_required(VERSION 3.10)
project(Team10)

set(CMAKE_CXX_STANDARD 11)

# Download and unpack googletest at configure time
configure_file(CMakeLists.txt.in googletest-download/CMakeLists.txt)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
        RESULT_VARIABLE result
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
if(result)
    message(FATAL_ERROR "CMake step for googletest failed: ${result}")
endif()
execute_process(COMMAND ${CMAKE_COMMAND} --build .
        RESULT_VARIABLE result
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
if(result)
    message(FATAL_ERROR "Build step for googletest failed: ${result}")
endif()

# Prevent overriding the parent project's compiler/linker
# settings on Windows
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# Add googletest directly to our build. This defines
# the gtest and gtest_main targets.
add_subdirectory(${CMAKE_CURRENT_BINARY_DIR}/googletest-src
        ${CMAKE_CURRENT_BINARY_DIR}/googletest-build
        EXCLUDE_FROM_ALL)

# The gtest/gtest_main targets carry header search path
# dependencies automatically when using CMake 2.8.11 or
# later. Otherwise we have to add them here ourselves.
if (CMAKE_VERSION VERSION_LESS 2.8.11)
    include_directories("${gtest_SOURCE_DIR}/include")
endif()

add_executable(Team10
        src/main.cpp
        #src/person_test.cpp
        #src/BST_test.cpp
        #src/BST_Person_Test.cpp
        src/Person.cpp
        src/BST.cpp
        src/Balanced_Tree.cpp
        src/tNode.cpp
        src/Member.cpp
        src/Provider.cpp
        src/Manager.cpp
        src/member_service.cpp
        src/provider_service.cpp
        src/service.cpp
        src/Terminal.cpp
        src/Controller.cpp
        src/Provider_Directory.cpp)

target_link_libraries(Team10 gtest_main)
add_test(NAME PersonTest COMMAND DefaultConstructor)
