cmake_minimum_required(VERSION 2.8)
project(Forward)

set(CMAKE_CXX_STANDARD 11)


find_package( OpenCV REQUIRED )
message("Open CV version is ${OpenCV_VERSION}")
# Uncomment for no display (e.g. AWS instance)
#set(Opencv_DEFINITIONS -DNO_DISPLAY)
# add_definitions(${Opencv_DEFINITIONS})
message("Opencv_DEFINITIONS is ${Opencv_DEFINITIONS}")
include_directories(${OPENCV_INCLUDE_DIRS})

add_executable(Forward_DAC main.cpp
        include/Network.cpp
        include/Network.h
        include/quantize.h
        src/image_proc.h
        net_def/DAC/DAC_include.h
        net_def/DAC/NETNAME_DAC.h
        src/string_op.h
        net_def/DAC/DAC_include2.h
        net_def/DAC/NetDAC.cpp
        net_def/DAC/NetDAC.h
        include/ImgLoader.cpp
        include/ImgLoader.h)
target_link_libraries(Forward_DAC -ljpeg)
#target_link_libraries(Forward_DAC ${OpenCV_LIBS})

add_executable(OpenCV_Image main_cv.cpp)
target_link_libraries(OpenCV_Image ${OpenCV_LIBS})

add_executable(ImageProc
        main_image.cpp
        src/image_proc.h
        include/ImgLoader.cpp
        include/ImgLoader.h)
target_link_libraries(ImageProc -ljpeg)
target_link_libraries(ImageProc ${OpenCV_LIBS})