cmake_minimum_required(VERSION 3.21)

project(
   glaze_example
   VERSION 0.0.1
   LANGUAGES CXX
)

file(GLOB srcs src/*.cpp include/*.hpp)

if(glaze_ERLANG_FORMAT)
  list(APPEND CMAKE_MODULE_PATH "${EXTERNAL_MODULE_PATH}")
  find_package(Erlang REQUIRED)
endif(glaze_ERLANG_FORMAT)

find_package(glaze CONFIG REQUIRED)

add_executable(${PROJECT_NAME} ${srcs})
target_include_directories(${PROJECT_NAME} PRIVATE include)
target_link_libraries(${PROJECT_NAME} PRIVATE glaze::glaze)

include(CTest)
add_test(NAME ${PROJECT_NAME}_test COMMAND ${PROJECT_NAME})
