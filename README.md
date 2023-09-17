# Build and run

Linux Desktop target:
```
mkdir build
cd build
cmake .. -G Ninja
ninja
./main
```

WASM target:
```
# Install Emscripten
mkdir build
cd build
emcmake cmake .. -G Ninja
ninja
# output is in web directory
```
