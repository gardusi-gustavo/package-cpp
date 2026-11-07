# cpp

C++ package template with a CMake build and a minimal test.

## Build

```bash
cmake -S . -B build
cmake --build build
ctest --test-dir build --output-on-failure
```
