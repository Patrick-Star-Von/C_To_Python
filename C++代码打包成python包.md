# 项目目录
![image](https://github.com/user-attachments/assets/e1d457a8-25fa-4ff8-8b4b-03b72a3ef0fa)


# 配置pyproject.toml
创建pyproject.toml，并输入以下内容：  
[build-system]
requires = ["scikit-build-core >=0.4.3", "nanobind >=1.3.2"]
build-backend = "scikit_build_core.build"

[project]
name = "mc33"
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
# Protect the configuration against future changes in scikit-build-core
minimum-version = "0.4"
# Setuptools-style build caching in a local directory
build-dir = "build/{wheel_tag}"
# Build stable ABI wheels for CPython 3.12+
wheel.py-api = "cp312"
