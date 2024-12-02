cmake_minimum_required(VERSION 3.16)
project(hiox)

set(CMAKE_CXX_STANDARD 17)

find_package(OpenCV REQUIRED)

# onnxruntime
#set(ONNXRUNTIME_ROOT ./onnxruntime-linux-x64-1.18.1)
set(ONNXRUNTIME_INCLUDE_DIRS ${ONNXRUNTIME_ROOT}/include)
set(ONNXRUNTIME_LIBS ${ONNXRUNTIME_ROOT}/lib/onnxruntime.so)

include_directories(
        ${ONNXRUNTIME_INCLUDE_DIRS}
        ${CMAKE_CURRENT_SOURCE_DIR}/src
)

set(LIBS
    ${OpenCV_LIBS}
    ${ONNXRUNTIME_LIBS}
)

file(GLOB_RECURSE SRC
        src/*.cc
        src/*.cpp
        src/*.h
        src/*.hpp
)

add_executable(DetectDemo DetectDemo.cc ${SRC})
target_link_libraries(DetectDemo ${LIBS})

add_executable(MatchDemo MatchDemo.cc ${SRC})
target_link_libraries(MatchDemo ${LIBS})

add_executable(FlowDemo FlowDemo.cc ${SRC})
target_link_libraries(FlowDemo ${LIBS})
