cmake_minimum_required(VERSION 2.8.3)
cmake_policy(SET CMP0020 NEW)
project(qt_gui_cpp)

find_package(catkin REQUIRED COMPONENTS cmake_modules pluginlib)
find_package(Boost REQUIRED COMPONENTS filesystem system)
if(WIN32)
  find_package(TinyXML2 REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS pluginlib
  CFG_EXTRAS ${PROJECT_NAME}-extras.cmake
  DEPENDS Boost TinyXML2
)
else()
  find_package(TinyXML REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
  CATKIN_DEPENDS pluginlib
  CFG_EXTRAS ${PROJECT_NAME}-extras.cmake
  DEPENDS Boost TinyXML
)
endif()

catkin_python_setup()
if(WIN32)
include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS} ${TinyXML2_INCLUDE_DIRS})
else()
include_directories(include ${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS} ${TinyXML_INCLUDE_DIRS})
endif()
add_subdirectory(src)

install(DIRECTORY include/qt_gui_cpp/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
install(FILES plugin.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
