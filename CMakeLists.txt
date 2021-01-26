cmake_minimum_required(VERSION 3.2)
if ($ENV{TRAVIS_BUILD_NUMBER})
    project(matrix VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})
else ()
    project(matrix VERSION 0.0.1)
endif()
add_executable(matrix main.cpp)
target_include_directories(matrix PRIVATE ${PROJECT_SOURCE_DIR})
set_target_properties(matrix PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON

)
if (MSVC)
    target_compile_options(matrix PRIVATE
        /W4
    )
else ()
    target_compile_options(matrix PRIVATE
        -Wall -Wextra -pedantic
        -Werror
    )
endif()
install(TARGETS matrix RUNTIME DESTINATION bin)
set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT example@example.com)

include(CPack)
#find_package(GTest REQUIRED)
###enable_testing()
##target_link_libraries(gtest_hw5
 ##  )
#target_link_libraries(gtest_hw5
#${CMAKE_THREAD_LIBS_INIT}
#)
##set_property(TARGET gtest_hw5 PROPERTY CXX_STANDARD 14)
