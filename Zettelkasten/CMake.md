#### 📝 Note: CMake 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚2:07 am  📆 Wed Jul 23
 🔗 **Related Concepts**: #projecttemplate
___
## ⚙️ CMake Basics – Minimal Reference


### 📂 Typical Project Structure


```title:tree
my-project/  
├── CMakeLists.txt  
├── src/  
│ └── main.cpp  
└── build/
```


---
### 📝 Minimal CMakeLists.txt


```title:FileContents
cmake_minimum_required(VERSION 3.16)
project(my_project LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(${PROJECT_NAME} src/main.cpp)
```


---
### 🏗️ Building the Project


```bash
mkdir -p build
cd build
cmake ..
make
```


---
### 🧠 Useful Tips
- Use `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` for editor integration
- `.gitignore` should exclude `build/`
- CMake does not build inside your source directory—always use `/build/`