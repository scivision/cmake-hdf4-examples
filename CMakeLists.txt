cmake_minimum_required(VERSION 3.19...3.24)

project(HDF4examples LANGUAGES C Fortran)

enable_testing()

include(FetchContent)

find_package(HDF4 CONFIG COMPONENTS C Fortran)

if(NOT HDF4_FOUND)
  set(HDF4_BUILD_FORTRAN on)

  FetchContent_Declare(hdf4
    URL https://github.com/HDFGroup/hdf4/releases/download/hdf4.3.0/hdf4.3.0.tar.gz
  )
  FetchContent_MakeAvailable(hdf4)
endif()

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
