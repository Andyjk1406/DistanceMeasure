cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

project(Distance)

find_package(VTK REQUIRED)
include(${VTK_USE_FILE})

find_package(PCL 1.7 REQUIRED)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
 
 
if (VTK_VERSION VERSION_LESS "8.90.0")
  # old system
  include(${VTK_USE_FILE})
  add_executable(Distance MACOSX_BUNDLE Distance.cpp)
  target_link_libraries(Distance PRIVATE ${PCL_LIBRARIES} ${VTK_LIBRARIES})
else ()
  # include all components
  add_executable(Distance MACOSX_BUNDLE Distance.cpp)
  target_link_libraries(Distance PRIVATE ${PCL_LIBRARIES} ${VTK_LIBRARIES})
  # vtk_module_autoinit is needed
  vtk_module_autoinit(
    TARGETS Distance
    MODULES ${VTK_LIBRARIES}
    )
endif () 