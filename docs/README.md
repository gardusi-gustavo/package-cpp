# cpp docs

Build the template with CMake:

```bash
cmake -S . -B build
cmake --build build
ctest --test-dir build --output-on-failure
```

See [`algorithms/README.md`](algorithms/README.md) for the imported C++17 algorithm archive.
