cmake_minimum_required(VERSION 3.14)
project(tigerbeetle-client LANGUAGES C)

include(FetchContent)
find_package(TigerBeetle QUIET)
if(NOT TigerBeetle_FOUND)
    FetchContent_Declare(TigerBeetle GIT_REPOSITORY https://github.com/kassane/tigerbeetle-cpp.git
        GIT_TAG main)
    FetchContent_GetProperties(TigerBeetle)
    # required
    set(APP_TARGETS ${PROJECT_NAME}) # executable or executables (need foreach) names
    FetchContent_MakeAvailable(TigerBeetle)
endif()

add_executable(${PROJECT_NAME} src/main.c)
target_link_libraries(${PROJECT_NAME}
    PRIVATE tb_client
)
target_include_directories(${PROJECT_NAME} PUBLIC ${tigerbeetle_SOURCE_DIR}/include)
target_link_directories(${PROJECT_NAME} PUBLIC ${tigerbeetle_BINARY_DIR})
