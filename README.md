# CMake HDF4 Examples

[![ci](https://github.com/scivision/cmake-hdf4-examples/actions/workflows/ci.yml/badge.svg)](https://github.com/scivision/cmake-hdf4-examples/actions/workflows/ci.yml)

Examples using CMake with HDF4 and Fortran.
This will build HDF4 if not present.

```sh
cmake -Bbuild
cmake --build build

ctest --test-dir build -L example -V
```
