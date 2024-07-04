cmake_minimum_required(VERSION 3.20)
project (EDIPIC-1D LANGUAGES C Fortran)

## set compiler
set(CMAKE_Fortran_COMPILER  mpifort)
set(CMAKE_C_COMPILER        mpicc)

## avoid the line length limit
set(CMAKE_Fortran_FLAGS     "-ffree-line-length-none -fallow-invalid-boz -w")

file(GLOB src_f_files "src/*90")
file(GLOB src_c_files "src/*.c")

## set MPICH library directories
set(mpi_DIR         ${MPICH_DIR})
set(INCLUDE_DIRS    ${INCLUDE_DIRS}     "${mpi_DIR}/include")
set(LINK_DIRS       ${LINK_DIRS}        "${mpi_DIR}/lib")
set(LINK_LIBS       ${LINK_LIBS}        "mpifort")

## compile the c library
add_library(randc  STATIC ${src_c_files})
## compile the fortran program
add_executable(${PROJECT_NAME} ${src_f_files})

## link the libraries
set(LINK_LIBS       ${LINK_LIBS}        randc)
target_include_directories  (${PROJECT_NAME} PUBLIC ${INCLUDE_DIRS})
target_link_directories     (${PROJECT_NAME} PUBLIC ${LINK_DIRS})
target_link_libraries       (${PROJECT_NAME} PUBLIC ${LINK_LIBS})
