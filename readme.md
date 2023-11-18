# 类似go mod 的 c++ 依赖管理模式，使用 vcpkg cmake manifest 管理依赖
参考： https://learn.microsoft.com/en-us/vcpkg/get_started/get-started?pivots=shell-bash

1. 安装 vcpkg
```shell
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg && ./bootstrap-vcpkg.sh
```
2. 设置 VCPKG_ROOT 和 vcpkg 的 执行文件PATH 变量
```shell
export VCPKG_ROOT=/path/to/vcpkg
export PATH=$VCPKG_ROOT:$PATH
```
3. 创建你的项目，然后使用 vcpkg
```shell
mkdir yourproject
cd yourproject
vcpkg new --application
```

4. 添加依赖, 例如 crow
```shell
vcpkg add port crow
```


5. 创建文件 CMakeLists.txt，之后根据 拉取依赖后的提示在 CMakeLists.txt 文件中添加 find 和 add 添加以下内容 websocketpp  包
```text
cmake_minimum_required(VERSION 3.10)

project(yourproject)

# Crow
find_package(Crow CONFIG REQUIRED)
target_link_libraries(apiserver PUBLIC Crow::Crow) # 添加 websocketpp 包的lib到要引入的文件
```

6. 创建项目 cmake 和 vcpkg 的关联配置文件 CMakePresets.json
> ${sourceDir} 
> $ENV{VCPKG_ROOT}
> Note：这两个变量需要替换成自己的实际目录
```
{
  "version": 3,
  "configurePresets": [
    {
      "name": "default",
      "binaryDir": "${sourceDir}/build",
      "cacheVariables": {
        "CMAKE_TOOLCHAIN_FILE": "$ENV{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake"
      }
    }
  ]
}
```

5. 拉取依赖
```shell
cmake --preset=default
```

6. 构建项目
```shell
cmake --build build
```

7. run 二进制文件
```shel
./build/apiserver
./build/ws
```