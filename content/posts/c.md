+++
title = "c"
author = ["PENG Kui"]
tags = ["PL", "c"]
draft = false
+++

## Coding Style {#coding-style}

-   缩进最好用 4 个空格
-   用全小写加下划线方式命名变量和函数
-   宏用全大写字母，自定义类型用驼峰命名方式
-   ...


## Example {#example}

```C
#include <stdio.h>

int main(int argn, char* argv[]) {
  int x, y;
  int i, j;
  for (i = 0; i < 3; i++) {
    for (j = 0; j < 3; j++) {
      if (i > j) {
        printf("%d > %d\n", i, j);
      }
    }
  }
  return 0;
}
```

```text
1 > 0
2 > 0
2 > 1
```


## Language {#language}

采用 c99 的语法。


## Tools {#tools}

clang-format
: `clang-format -style=Google -dump-config > .clang-format`
    导出 Google 风格的 format 配置。


## 参考链接 {#参考链接}

-   clang-format <https://releases.llvm.org/11.0.0/tools/clang/docs/ClangFormatStyleOptions.html>
