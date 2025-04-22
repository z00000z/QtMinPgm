cmake_minimum_required(VERSION 3.10)
project(QtMinPgm VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# build type
if(DEFINED CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE} CACHE STRING "Set to either \"Release\" or \"Debug\"")
else()
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Set to either \"Release\" or \"Debug\"")
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
else()
    set(CMAKE_WIN32_EXECUTABLE ON)
endif()

# undefined reference to `vtable for mainwindow'
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)

set(PROJECT_NAME QtMinPgm)

set(SOURCE_DIR src)
set(SOURCE_FILE
    ${SOURCE_DIR}/main.cpp
    ${SOURCE_DIR}/mainwindow.h
    ${SOURCE_DIR}/mainwindow.cpp
    ${SOURCE_DIR}/mainwindow.ui
)

# 查找 Qt6 库
find_package(Qt6 REQUIRED COMPONENTS Core Gui Widgets)

# 添加可执行文件
add_executable(${PROJECT_NAME} ${SOURCE_FILE})

#
target_include_directories(${PROJECT_NAME} PRIVATE include)

# 链接 Qt6 库
target_link_libraries(${PROJECT_NAME}
    PRIVATE

    # Qt6::Core
    # Qt6::Gui
    Qt6::Widgets
)

# 添加安装规则
install(TARGETS ${PROJECT_NAME}
    DESTINATION ${CMAKE_INSTALL_BINDIR}
    COMPONENT binary
)

# 输出编译器信息
message(STATUS "CXX compiler: ${CMAKE_CXX_COMPILER}")
message(STATUS "CXX compiler version: ${CMAKE_CXX_COMPILER_ID} ${CMAKE_CXX_COMPILER_VERSION}")
message(STATUS "C compiler: ${CMAKE_C_COMPILER}")
message(STATUS "C compiler version: ${CMAKE_C_COMPILER_ID} ${CMAKE_C_COMPILER_VERSION}")
