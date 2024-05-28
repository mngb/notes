+++
title = "sass"
author = ["PENG Kevin"]
tags = ["css", "scss", "sass"]
draft = false
+++

## 语法 {#语法}

类型
: -   数字 `1pt`, `10.0`
    -   字符串 `'aa'`, `"aa"`,=aa=
    -   布尔 `false`, `true`
    -   数组 `a b`, `a, b`
    -   颜色 `rgb(255,255,255)`, `#ffffff`
    -   空 `null`
    -   map `{a: b}`

变量 `$` 前缀
    ```scss
    $var: "default"
    ```

占位符选择器 `%`

嵌套
    -   语法嵌套
        ```scss
        .class {
            .class2 {
                }
            }
        ```
    -   属性嵌套
        ```scss
        font: {
            family: song
            }
        ```


&amp; 引用父选择器

@mixin

@include mixin

@import 文件
    ```scss
    @import "a.scss";
    ```


partial (_xxx.scss 用 import xxx 表示)

@extend 选择器

函数
    预定义函数列表 <https://sass-lang.com/documentation/modules>
    ```scss
    @function funcname($param) {
        @return xxx;
    }
    ```


插值 #{}

@if
    ```scss
    @if $type==ocean {
        color: blue;
    } @else if $type==matador {
        color: red;
    } @else {
        color: black;
    }
    ```


@each
    `@each $animal in puma, sea {}`

@for
    1..3:
    `@for $i from 1 through 3 {}`
    `@for $i from 1 to 4 {}`

@while
    `@while $i > 0 {}`

@debug @warn
    `@debug "Debug info";`


## 小技巧 {#小技巧}

自动编译
: -   单个文件 `sass --watch input.scss:output.css`
    -   目录 `sass --watch inputFolder:outputFolder`
