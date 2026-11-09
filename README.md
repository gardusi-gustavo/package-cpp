# package-cpp

C++20 package with a CMake build, a minimal library, and the imported C++17
algorithm archive.

## Layout

| Path | Holds |
| --- | --- |
| `src/gardusi_gustavo.cpp` | publishable library |
| `src/algorithms/` | reference algorithms and contest solutions |
| `docs/algorithms/` | algorithm handbook |

## Build

```bash
cmake -S . -B build
cmake --build build
ctest --test-dir build --output-on-failure
```

The fallback `infra/scripts/compile-algorithms.sh` compiles every algorithm with
`g++ -std=c++17` when CMake is unavailable.
