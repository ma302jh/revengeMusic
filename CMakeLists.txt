cmake_minimum_required (VERSION 2.8)
project (revengeMusic)

include_directories("${CMAKE_SOURCE_DIR}/include/")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")
SET(GCC_COVERAGE_COMPILE_FLAGS "-std=c++11")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GCC_COVERAGE_COMPILE_FLAGS}" )

#Find FMOD
find_package(FMOD)
IF(FMOD_FOUND)
  include_directories(${FMOD_INCLUDE_DIRS})
ELSEIF(NOT WIN32)
  include_directories(${PROJECT_BINARY_DIR}/fmod/api/lowlevel/inc)
ENDIF(FMOD_FOUND)

add_executable(
  revengeMusic
  src/main.cpp
  src/IPC.cpp
  src/Sound.cpp
)

IF(FMOD_FOUND)
  target_link_libraries(revengeMusic ${FMOD_LIBRARIES})
ELSEIF(NOT WIN32)
  target_link_libraries(revengeMusic ${PROJECT_BINARY_DIR}/fmod/api/lowlevel/lib/x86_64)
ENDIF(FMOD_FOUND)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "build/")