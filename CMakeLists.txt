cmake_minimum_required(VERSION 3.26...4.5)

project(HDF4examples LANGUAGES C Fortran)

enable_testing()

include(FetchContent)

set(HDF4_BUILD_FORTRAN on)
set(CMAKE_Fortran_MODULE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/include) # HDF4 4.4.0 needs this set to something

set(CMAKE_PROJECT_HDF4_INCLUDE "${CMAKE_CURRENT_LIST_DIR}/cmake/hdf4-compiler-options.cmake")

FetchContent_Declare(hdf4
URL https://github.com/HDFGroup/hdf4/releases/download/hdf4.4.0/hdf4.4.0.tar.gz
CMAKE_ARGS -DCMAKE_BUILD_TYPE=Release
FIND_PACKAGE_ARGS CONFIG COMPONENTS C Fortran
)
FetchContent_MakeAvailable(hdf4)

set_property(DIRECTORY PROPERTY LABELS example)

add_executable(h4ex_VD_write_to_vdata test/h4ex_VD_write_to_vdata.f)
target_link_libraries(h4ex_VD_write_to_vdata PRIVATE hdf_fortran-static)

add_test(NAME h4ex_VD_write_to_vdata COMMAND h4ex_VD_write_to_vdata)
set_tests_properties(h4ex_VD_write_to_vdata PROPERTIES
  FIXTURES_SETUP vdata
)

add_executable(h4ex_VD_read_from_vdata test/h4ex_VD_read_from_vdata.f)
target_link_libraries(h4ex_VD_read_from_vdata PRIVATE hdf_fortran-static)

add_test(NAME h4ex_VD_read_from_vdata COMMAND h4ex_VD_read_from_vdata)
set_tests_properties(h4ex_VD_read_from_vdata PROPERTIES
  FIXTURES_REQUIRED vdata
)

file(GENERATE OUTPUT .gitignore CONTENT "*")
