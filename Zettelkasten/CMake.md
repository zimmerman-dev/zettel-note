#### 📝 Note: CMake 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:07 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #cpp #toolchain #note
___
## ⚙️ CMake Basics – Minimal Reference
### 📂 Typical Project Structure
```title:tree
├── assets
│   └── asset.jpg
├── CMakeLists.txt
├── LICENSE
├── README.md
└── src
    ├── header.cpp
    ├── header.h
    ├── main.cpp

```
### 📝 Minimal CMakeLists.txt
```title:FileContents
cmake_minimum_required(VERSION 3.16)

# -------------------------------
# Project Configuration
# -------------------------------

# Set your project name — this becomes the output binary name
project(<your_project_name> LANGUAGES CXX)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# -------------------------------
# External Dependencies (System)
# -------------------------------

# Use find_package() for system-installed libraries
# Example:
# find_package(spdlog REQUIRED)
# target_link_libraries(${PROJECT_NAME} PRIVATE spdlog::spdlog)

# -------------------------------
# External Dependencies (Vendored)
# -------------------------------

# Use add_subdirectory() if you include third-party code in your project tree
# Example:
# add_subdirectory(external/fmt)
# target_link_libraries(${PROJECT_NAME} PRIVATE fmt::fmt)

# -------------------------------
# Build Targets
# -------------------------------

# Define your main executable
add_executable(${PROJECT_NAME} src/main.cpp)

# Link additional libraries here
# target_link_libraries(${PROJECT_NAME} PRIVATE your_library::your_library)
```
### 🏗️ Building the Project
```bash
mkdir -p build
cd build
cmake ..
make


//OR
// Project specific with CMake
cmake -S . -B build
cmake --build build

```
### 🏗️ Clean rebuild
```bash
rm -rf build
mkdir build
cd build
cmake ..
cmake --build .
```
### 🧠 Useful Tips
- Use `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` for editor integration
- `.gitignore` should exclude `build/`
- CMake does not build inside your source directory—always use `/build/`
