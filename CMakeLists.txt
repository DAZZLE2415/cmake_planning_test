cmake_minimum_required(VERSION 3.22.1)
project(planning)

set(CMAKE_CXX_STANDARD 17)

# 输出路径
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

# 添加源文件
set(SRC_LISTS
  src/pnc_map.cpp
  src/process.cpp
)

# 构建共享库
add_library(common SHARED ${SRC_LISTS})

# 设置头文件搜索路径
target_include_directories(common PUBLIC ${PROJECT_SOURCE_DIR}/include)

# 添加可执行程序
add_executable(planning_main planning_main.cpp) # pnc_map.cpp 和 process.cpp 经在 common 库
target_include_directories(planning_main PUBLIC ${PROJECT_SOURCE_DIR}/include)

# 链接共享库
target_link_libraries(planning_main PUBLIC common)
