cmake_minimum_required(VERSION 3.10)
project (EDIPIC-1D LANGUAGES C Fortran)
set(LIB_NAME ${LIB_NAME} RAND_C_LIBRARY)

set(CMAKE_Fortran_COMPILER mpiifort)
set(CMAKE_C_COMPILER gcc)

file(GLOB src_f_files "src/*.f90")
file(GLOB src_c_files "src/*.c")

add_library(${LIB_NAME} STATIC ${src_c_files})
add_executable(${PROJECT_NAME} ${src_f_files})

target_include_directories  (${PROJECT_NAME} PUBLIC ${INCLUDE_DIRS})
target_link_directories     (${PROJECT_NAME} PUBLIC ${LINK_DIRS})
target_link_libraries       (${PROJECT_NAME} PUBLIC ${LINK_LIBS} ${LIB_NAME})
