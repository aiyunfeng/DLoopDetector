project(dloopdetector)
cmake_minimum_required(VERSION 2.8.3)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

add_definitions(-std=c++11)

cs_add_executable(demo_brief demo/demo_brief.cpp)

cs_add_executable(demo_surf demo/demo_surf.cpp)

set(RESOURCE_FILE ${CMAKE_BINARY_DIR}/resources.tar.gz)
if(NOT EXISTS ${CMAKE_BINARY_DIR}/resources/)
  if(NOT EXISTS ${RESOURCE_FILE})
    file(DOWNLOAD http://doriangalvez.com/resources/DLoopDetector/resources.tar.gz 
      ${RESOURCE_FILE} STATUS status SHOW_PROGRESS EXPECTED_MD5 c001da68ddaceed1de9c16aaac22ed80)
  endif(NOT EXISTS ${RESOURCE_FILE})
  execute_process(COMMAND ${CMAKE_COMMAND} -E tar xzf ${RESOURCE_FILE})
  file(REMOVE ${RESOURCE_FILE})
endif(NOT EXISTS ${CMAKE_BINARY_DIR}/resources/)

cs_install()
cs_export()
