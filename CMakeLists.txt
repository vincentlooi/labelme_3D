cmake_minimum_required(VERSION 2.6 FATAL_ERROR)

project(data3D)

set(CXX_COMPILE_FLAGS "-std=c++11 -w")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${CXX_COMPILE_FLAGS}")


find_package(PCL 1.8 REQUIRED)
find_package(OpenCV REQUIRED)
find_package(Eigen3)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

include_directories(include)
include_directories(include/utils)

add_executable (pinhole_test ../test/pinhole_test.cpp)
target_link_libraries (pinhole_test ${PCL_LIBRARIES} ${OpenCV_LIBS})

add_executable (labelme_3d ../test/labelme_3d.cpp ../src/pcl_viewer_custom.cc ../src/labelme_io.cc)
target_link_libraries (labelme_3d ${PCL_LIBRARIES} ${OpenCV_LIBS} "-lpthread")

add_executable (read_labelme_data ../test/read_labelme_data.cpp ../src/labelme_io.cc)
target_link_libraries (read_labelme_data ${PCL_LIBRARIES} ${OpenCV_LIBS})

#add_executable (cvui_test ../test/cvui_test.cpp)
#target_link_libraries (cvui_test ${OpenCV_LIBS})

#add_executable (pcl_viewer_test ../test/pcl_viewer_test.cpp ../src/pcl_viewer_custom.cc)
#target_link_libraries (pcl_viewer_test ${PCL_LIBRARIES})
