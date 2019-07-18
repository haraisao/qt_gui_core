cmake_minimum_required(VERSION 2.8.3)
project(qt_gui_app)

find_package(catkin REQUIRED)
catkin_package()

catkin_python_setup()

install(PROGRAMS scripts/qt_gui_app
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
if(WIN32)
 install_python_cli(qt_gui_app)
endif()