cmake_minimum_required(VERSION 2.8.3)
project(camera_info_manager_py)

find_package(catkin REQUIRED COMPONENTS camera_info_manager roscpp sensor_msgs)

catkin_python_setup()
catkin_package(CATKIN_DEPENDS camera_info_manager roscpp sensor_msgs)

# Unit test uses nose, but needs rostest to create a ROS environment.
if (CATKIN_ENABLE_TESTING)
  add_executable(generate_camera_info
    tests/generate_camera_info.cpp
    )
  target_include_directories(generate_camera_info
    PRIVATE
    ${catkin_INCLUDE_DIRS}
    )
  target_link_libraries(generate_camera_info
    ${catkin_LIBRARIES}
    )

  find_package(rostest REQUIRED)

  add_rostest(tests/load_cpp_camera_info.test DEPENDENCIES generate_camera_info)
  add_rostest(tests/unit_test.test)
endif(CATKIN_ENABLE_TESTING)
