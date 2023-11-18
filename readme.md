# 使用 vcpkg cmake manifest 管理依赖
```shell
# 初始化项目 https://learn.microsoft.com/en-us/vcpkg/get_started/get-started?pivots=shell-bash
vcpkg new --application

# 添加依赖
vcpkg add port crow

# 拉取依赖
cmake --preset=default

# 之后根据 拉取依赖后的提示在 CMakeLists.txt 文件中添加 find 和 add
>
# 添加 websocketpp  包
find_package(websocketpp CONFIG REQUIRED) // 查找包
target_link_libraries(ws PRIVATE websocketpp::websocketpp) 添加 websocketpp 包的lib到要引入的文件


# 构建项目
cmake --build build
```

## examples apiserver
