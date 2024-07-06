cmake_minimum_required(VERSION 3.20)
project (EDIPIC-1D LANGUAGES C Fortran)

## set compiler
set(CMAKE_Fortran_COMPILER  mpiifort)
set(CMAKE_C_COMPILER        gcc)

file(GLOB src_f_files "src/*90")
file(GLOB src_c_files "src/*.c")

## compile the c library
add_library(RAND_C STATIC ${src_c_files})
set(LIB_NAME ${LIB_NAME} RAND_C)

## compile the fortran program
add_executable(${PROJECT_NAME} ${src_f_files})

## link the libraries
target_include_directories  (${PROJECT_NAME} PUBLIC ${INCLUDE_DIRS})
target_link_directories     (${PROJECT_NAME} PUBLIC ${LINK_DIRS})
target_link_libraries       (${PROJECT_NAME} PUBLIC ${LINK_LIBS} ${LIB_NAME})
