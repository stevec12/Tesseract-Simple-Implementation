cmake_minimum_required(VERSION 3.10)

#set project name and version
project(SimpleTesseract VERSION 1.0)

#add executable 
add_executable(SimpleTesseract main.cxx)

#specify C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

#Leptonica Setup
find_package(Leptonica REQUIRED)
include_directories(${Leptonica_INCLUDE_DIRS})
target_link_libraries(SimpleTesseract PUBLIC ${Leptonica_LIBRARIES})

#Tesseract Setup
find_package(Tesseract REQUIRED)
target_link_libraries(SimpleTesseract PUBLIC Tesseract::libtesseract)

#set tessdata path 
set(TESSDATA_PATH "C:\\Program Files (x86)\\tesseract\\lib")

#config header file to pass version number and tessdata folder location to source code
configure_file(SimpleTesseractConfig.h.in SimpleTesseractConfig.h)

target_include_directories(SimpleTesseract PUBLIC
"${PROJECT_BINARY_DIR}"
"${Tesseract_INCLUDE_DIRS}"
"${Leptonica_INCLUDE_DIRS}"
)