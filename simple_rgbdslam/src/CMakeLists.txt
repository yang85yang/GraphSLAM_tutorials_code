message("src cmake ")

# find pcl
find_package(PCL 1.7 REQUIRED)
message("pcl lib is found:"${PCL_INCLUDE_DIRS})
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
ADD_DEFINITIONS(${PLC_DEFINITIONS})
# find opencv
find_package(OpenCV 2.4 REQUIRED)
include_directories(${OPENCV_INCLUDE_DIRS})

LIST(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules)
# find g2o
find_package(G2O REQUIRED)
IF(G2O_FOUND)
    include_directories(${G2O_INCLUDE_DIR})
ENDIF(G2O_FOUND)
find_package(Eigen3 REQUIRED)
find_package(CSparse REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR} ${CSPARSE_INCLUDE_DIR})
SET(G2O_LIBS g2o_cli g2o_ext_freeglut_minimal g2o_simulator g2o_solver_slam2d_linear g2o_types_icp g2o_types_slam2d g2o_core g2o_interface g2o_solver_csparse g2o_solver_structure_only g2o_types_sba g2o_types_slam3d g2o_csparse_extension g2o_opengl_helper g2o_solver_dense g2o_stuff g2o_types_sclam2d g2o_parser g2o_solver_pcg g2o_types_data g2o_types_sim3 cxsparse )


add_library(RgbdSlamlib FrameData.cpp FrameData.h)
target_link_libraries(RgbdSlamlib ${PCL_LIBRARIES} ${OpenCV_LIBS} ${G2O_LIBS})
    
add_executable(rgbdslam main.cpp)
target_link_libraries(rgbdslam RgbdSlamlib)


