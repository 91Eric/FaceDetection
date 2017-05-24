cmake_minimum_required(VERSION 3.5.1)
if(COMMAND cmake_policy)
      cmake_policy(SET CMP0005 NEW)
endif(COMMAND cmake_policy)


SET(CUDA_LIBS_DIRS "/usr/ocal/cuda-8.0/lib64")

AUX_SOURCE_DIRECTORY(. DIR_SRCS)
ADD_EXECUTABLE(face ${DIR_SRCS})

FIND_PACKAGE(OpenCV REQUIRED) 
IF(OpenCV_FOUND)
    MESSAGE(STATUS "OPENCV is Found")
ELSE(OpenCV_FOUND)
    MESSAGE(WARNING "OPENCV isn't Found,Please install opencv!!")
ENDIF(OpenCV_FOUND)

#seetaface  INCLUDEDIR SET
INCLUDE_DIRECTORIES("${PROJECT_SOURCE_DIR}/include/identificationcinlude")


LINK_DIRECTORIES("/usr/local/lib" "${PROJECT_SOURCE_DIR}/lib")   


TARGET_LINK_LIBRARIES(face  -lopencv_cudabgsegm -lopencv_cudaobjdetect -lopencv_cudastereo -lopencv_shape -lopencv_stitching -lopencv_cudafeatures2d -lopencv_superres -lopencv_cudacodec -lopencv_videostab -lopencv_cudaoptflow -lopencv_cudalegacy -lopencv_calib3d -lopencv_features2d -lopencv_objdetect -lopencv_highgui -lopencv_videoio -lopencv_photo opencv_imgcodecs -lopencv_cudawarping -lopencv_cudaimgproc -lopencv_cudafilters -lopencv_video -lopencv_ml -lopencv_imgproc -lopencv_flann -lopencv_cudaarithm -lopencv_core -lopencv_cudev -lopencv_hal   seeta_facedet_lib seeta_fa_lib ) #此处使用OpenCV_LIBRARIES出错，原因未知

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

