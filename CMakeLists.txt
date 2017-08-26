cmake_minimum_required(VERSION 2.4.6)
project(bag_from_images)

set(CMAKE_BUILD_TYPE Release)

find_package(OpenCV REQUIRED)
find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  dynamic_reconfigure
  sensor_msgs
  roscpp
  rosbag
  roslib
  image_transport
  cmake_modules
)

catkin_package(
  INCLUDE_DIRS 
  LIBRARIES ${PROJECT_NAME}
  DEPENDS ${OPENCV_INCLUDE_DIR}
  )

include_directories(${catkin_INCLUDE_DIRS} 
		    ${OPENCV_INCLUDE_DIR}
		    )

# Sources files
set(SOURCE_FILES         
  Thirdparty/DLib/FileFunctions.cpp
)

add_executable(${PROJECT_NAME} main.cc ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME}
${OpenCV_LIBS}
		      ${catkin_LIBRARIES} 
${OPENCV_INCLUDE_DIR})
