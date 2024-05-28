+++
title = "yaml"
author = ["PENG Kevin"]
draft = false
+++

## 基本语法 {#基本语法}


### 基本类型 {#基本类型}

字符串
: 如 `"\n"`, `'\'`, `xx`

布尔值
: `true` 或 `false`

整数
: 如 `10`, `0xb`

浮点数
: 如 `1.0`, `1e+10`, `.inf`, `.NaN`

null
: 用 `~` 表示

日期
: 如 `2022-09-10`

时间
: 如 `2001-12-14t21:59:43.10-05:00`, iso8601 格式

数组
: 可写成 `[1,2]` 或 用 `-` 符号逐行写

Hash
: 可写成 `{1:2}` 或 用 `key: value` 逐行写
    `!!set` 无序 set
    ```yaml
    --- !!set
    ? ItemA
    ? ItemB
    ? ItemC
    ```
    `!!omap` 有序 map
    ```yaml
    --- !!omap
    ​- key1: 1
    ​- key2: 2
    ​- key3: 3
    ```


### 常用语法 {#常用语法}

转换类型
: 如 `!!str` 强制转为字符串类型

多行字符串
: 用 `|` , 保留多行换行符
    `|+` 保留段落末尾所有换行符， `|-` 删除段落末尾换行符

引用
: 用 `&<Name>` 设置被引用位置， 用 `*<Name>` 引用


## 举例 {#举例}

```yaml
UserName: Redef
Email: &email
  kevin.remegame@gmail.com
Languages:
  - Ruby
  - C
  - Haskell
  - Rust
Contact: *email
Experience: |
  1 years Haskell
  1 years Linux

StartWork: !!str 2012-07-01
```


## 参考文档 {#参考文档}

标准文档 [yaml_1_2.pdf](/ox-hugo/yaml_1_2.pdf)
