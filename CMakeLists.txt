cmake_minimum_required(VERSION 2.8)
project(SSFLLG)

enable_testing()

# Detect MPI. Can set MPI_LIBRARY and MPI_INCLUDE_PATH to work around.
include(FindMPI)
if(NOT MPI_FOUND)
  message(FATAL_ERROR "Unable to continue without MPI.")
endif(NOT MPI_FOUND)
include_directories(SYSTEM ${MPI_INCLUDE_PATH})

# Detect FFTW3
include(FindPkgConfig)
pkg_check_modules(FFTW REQUIRED fftw3)

add_subdirectory(dSFMT)

add_library(fft_ser STATIC fft_ser.c)
add_library(fft_par STATIC fft_par.c)

add_subdirectory(tests)
