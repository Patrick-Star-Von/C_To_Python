# 项目目录
![image](https://github.com/user-attachments/assets/e1d457a8-25fa-4ff8-8b4b-03b72a3ef0fa)


# 配置pyproject.toml
创建pyproject.toml，并输入以下内容：  
[build-system]  
requires = ["scikit-build-core >=0.4.3", "nanobind >=1.3.2"]  
build-backend = "scikit_build_core.build"  
  
[project]（项目基本信息）  
name = "mc33"（项目名字）  
version = "0.0.1"  
description = "A brief description of what this project does"  
readme = "README.md"  
requires-python = ">=3.8"  
authors = [  
{ name = "White Water", email = "981149199@qq.com" },  
]  
classifiers = [  
"License :: BSD",  
]  
  
[tool.scikit-build]  
#Protect the configuration against future changes in scikit-build-core  
minimum-version = "0.4"  
#Setuptools-style build caching in a local directory  
build-dir = "build/{wheel_tag}"  
#Build stable ABI wheels for CPython 3.12+  
wheel.py-api = "cp312"  

# 创建README.md
填入项目说明即可。  

# 配置CMakeLists.txt
配置如下：  
cmake_minimum_required(VERSION 3.15...3.30)  
project(pybind)  
  
set(Python_EXECUTABLE "E:/miniconda/python")  
set(Python_INCLUDE_DIRECTORY "E:/miniconda/include/Python")  
  
if (CMAKE_VERSION VERSION_LESS 3.18)  
set(DEV_MODULE Development)  
else()  
set(DEV_MODULE Development.Module)  
endif()  
  
find_package(Python 3.8 COMPONENTS Interpreter ${DEV_MODULE} REQUIRED)  
  
if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)  
set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build." FORCE)  
set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "MinSizeRel" "RelWithDebInfo")  
endif()  
  
# Detect the installed nanobind package and import it into CMake  
execute_process(  
COMMAND "${Python_EXECUTABLE}" -m nanobind --cmake_dir  
OUTPUT_STRIP_TRAILING_WHITESPACE OUTPUT_VARIABLE nanobind_ROOT)  
find_package(nanobind CONFIG REQUIRED)  
  
# Bind source files  
nanobind_add_module(pybind NOMINSIZE src/pybind.cpp)  
nanobind_add_module(testbind NOMINSIZE src/testbind.cpp)  
nanobind_add_module(mc33 NOMINSIZE src/mc33/libMC33++.cpp)  
  
install(TARGETS mc33 LIBRARY DESTINATION mc33)（前包，后library，表示把哪个包的东西打进library中）  

# 安装依赖
1.pyproject.toml中写的东西是打出来的包所需要的依赖信息，之后通过pip install可从中知道要安装什么。  
2.conda进入该项目目录，并调用pip install . 来安装依赖。  
![image](https://github.com/user-attachments/assets/f0484dd9-3966-4b80-99c1-67db0cfb525c)
