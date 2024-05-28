+++
title = "python style"
author = ["PENG Kui"]
draft = false
+++

## 参考 {#参考}

-   pep8 <https://peps.python.org/pep-0008/> 2001


## 规范 {#规范}


#### 命名 {#命名}

-   常量 CONST
-   类名 ClassName
-   函数名 func_name
-   变量名 var_name
-   模块名 mod_name
-   包名 packagename
-   异常名 ExceptionNameError (Error suffix)
-   类属性 \_attr_name ( with _ preffix)


#### 排版 {#排版}

-   缩进
-   tabsize 4
-   断行 行最大长度 79, 断行时考虑对齐和操作符
-   空格
    1.  '([{' 后不加空格
    2.  '=' unannotated function parameter(无类型声名) 左右不加空格，但 annotated
        parameter 左右加空格
-   换行 函数定义，类定义，代码块等
-   encoding 不加 encoding 声名


#### 注释 {#注释}

-   行内注释 '#' 少用，和表达式至少间隔 2 个空格
-   块注释
-   文档注释

    -   '''Summary

        Detail.

    '''

    1.  为公开的文档，方法和类编写该注释
    2.  开始部分一行描述
    3.  结尾 ''' 单独占一行
-   注释规范 <https://peps.python.org/pep-0257/>
-   其它注释提取规范


#### 程序 {#程序}

-   字符串引用 '' 和 "" 无区别，保持风格统一
-   import, 一行只有一个 module
-   try, try 中代码块尽量少
-   with, 资源只在该块代码中使用时
-   isinstance, 使用 isinstance 而不是 type 判断变量类型
-   isempty, 字符串，数组等空可直接写为表达式
    'if []' 而不是 'if len([])==0'
-   bool, 直接写，不需要再加 "=="
    'if True' 而不是 'if True==True'


## 检查工具 {#检查工具}

`pep8` `flake8` `pylint` 等
emacs 环境已配置好，在 `elpy-check` 命令中，对应 key-board `M-y c`
