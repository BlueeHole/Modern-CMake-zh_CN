# 导出和安装

要想让其他人使用你的库，有三种推荐的方法和一种不推荐的方法可供选择：

## FindModule脚本 (不推荐的方法)

作为库开发者，不要使用`Find<mypackage>.cmake`脚本，因为它是为不支持CMake的库所设立的。相反，应该使用`Config<mypackage>.cmake`。

## 添加子项目
一个软件包可以在一个子目录中包含你的项目，然后使用`add_subdirectory`来添加整个子目录。这对仅有头文件和快速编译的库很有用。注意，为了防止`install`命令干扰父项目，你可以在`add_subdirectory`命令中添加`EXCLUDE_FROM_ALL`；你明确使用的目标仍然会被构建。

为了支持这一点，作为库作者，你需要确保使用`CMAKE_CURRENT_SOURCE_DIR`而不是`PROJECT_SOURCE_DIR`（同样也适用于其他变量，如二进制目录相关）。你可以勾选`CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME`，以便只在这个项目中添加有意义的选项或默认值。

此外，为了发挥命名空间的作用，以及保持你的CMake配置的一致性，你应该添加

```cmake
add_library(MyLib::MyLib ALIAS MyLib)
```

`ALIAS`目标将不会被导出。

## 导出

第三种方法是`*Config.cmake`脚本，将会在本部分的下一章中涉及。
