+++
title = "cpp"
author = ["PENG Kevin"]
tags = ["PL", "cpp"]
draft = false
+++

## coding style {#coding-style}


### google cpp coding style {#google-cpp-coding-style}

<https://google.github.io/styleguide/cppguide.html>


## language {#language}

-   c++11
-   c++14
-   c++17


### hello world {#hello-world}

```cpp
#include <iostream>
int main()
{
  std::cout<<"Hello world";
  return 0;
}
```


## emacs environment {#emacs-environment}


### cmake 项目生成 {#cmake-项目生成}

1.  在 CMakeLists.txt 中加上 `set(CMAKE_EXPORT_COMPILE_COMMANDS ON)`
    加 `SET(CMAKE_BUILD_TYPE "Debug")` 可以编译时生成调试信息
2.  重新执行 `cmake ..`, 会在 build 目录生成 `compile_commands.json`
3.  将 `compile_commands.json` 拷贝到源代码目录，
    注意查看 emacs 中 `*clangd::stderr*` 的输出，会提示是否找到对应的
    `buiding file` .
