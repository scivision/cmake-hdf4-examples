# CMake HDF4 Examples

Examples using CMake with HDF4 and Fortran.
This will build HDF4 if not present.

```sh
cmake -Bbuild
cmake --build build

ctest --test-dir build -L example -V
```
