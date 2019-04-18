cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

project(Distance)

find_package(VTK REQUIRED)
include(${VTK_USE_FILE})

find_package(PCL 1.7 REQUIRED REQUIRED COMPONENTS io registration segmentation visualization)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
 
add_executable (Distance Distance.cpp)
 
if(VTK_LIBRARIES)
  target_link_libraries(Distance ${PCL_LIBRARIES} ${VTK_LIBRARIES})
else()
  target_link_libraries(Distance ${PCL_LIBRARIES} vtkHybrid vtkWidgets)
endif()