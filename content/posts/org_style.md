+++
title = "org style"
author = ["PENG Kevin"]
tags = ["style", "org", "org-mode"]
draft = false
+++

## 文件结构 {#文件结构}

优先使用 headline, 而不是列表，因为可形成目录结构


### roam 笔记结构 {#roam-笔记结构}

-   尽可能使用 tag
-   使用已定义 roam 结点
-   记录时完善网状结构


### 文章结构 {#文章结构}

-   使用 `coding: utf-8` 用 utf-8 编码文件
-   使用 `options: toc:t` 启用目录
-   使用 `include: <file>` 包含文件
-   -   `title`
    -   `author`
    -   `email`
    -   `language`
    -   `export_file_name`


## 标题段落 {#标题段落}

使用 `option: num:<N>` 控制显示标题深度。


### 标题 1 {#标题-1}


### 标题 2 {#标题-2}


## 列表 {#列表}


### 无序列表 {#无序列表}

start with `-` or `+`


### 有序列表 {#有序列表}

start with  `1.` or `1)`


### 名称列表 {#名称列表}

start with `<name> ::`


## 转义文本 {#转义文本}


### 段落 {#段落}

```text

```

`VERSE`, `QUOTE` , `CENTER` 同样可以用


### 字符 {#字符}

用 `X` 代替空字符，如： [X[1,2]], 将显示为：

```text
[[1,2]]
```


## horizontal ruler {#horizontal-ruler}

使用 `-----`


## latex embedded {#latex-embedded}

\\(a^2=b\\), 行内嵌入，use `org-preview-latex` to preview
\\[a^2 = b\\], 行间嵌入。


## 图片和链接 {#图片和链接}


### inline image and noninline image {#inline-image-and-noninline-image}

在 STARTUP 中设置 `inlineimages` 或设置变量 `org-startup-with-inline-images`


### image {#image}

<a id="org69e6b7d"></a>

![](/ox-hugo/example.jpg)
若要在文档中显示成图片，不能为 link 添加 description, 不然会显示成链接。
如 [description](/ox-hugo/example.jpg) 不会显示图片。
通过 `image-file-name-extensions` 和 `image-file-name-regexps` 可以控制识别
成图片的文件模式。


### link {#link}


#### 外部链接 {#外部链接}

使用 `[[hyper-link][description]]` 格式，因为 [hugo]({{< relref "hugo.md" >}}) 生成的 md 文件中
若没有 description, hyper-link 将无法通过网页访问。


#### 内部链接 {#内部链接}

用 `<<link>>` 标注位置，使用 `[[link][description]]` 引用。


## 表格 {#表格}

<a id="table--table-name"></a>
<div class="table-caption">
  <span class="table-number"><a href="#table--table-name">Table 1</a>:</span>
  table caption
</div>

| Col1 | Col2 |
|------|------|
| v1   | v2   |


## 程序和代码 {#程序和代码}


### C {#c}

```C
#include <stdio.h>
int main()
{
  printf("Hello C World!\n");
}
```

```text
Hello C World!
```


### rust {#rust}

```rust
println!("Hello Rust World!");
// https://github.com/brotzeit/rustic#org-babel
```

```text
Hello Rust World!
```


### CPP {#cpp}

```cpp
#include <iostream>
int main()
{
  std::cout<<"Hello CPP World";
  return 0;
}
```

```text
Hello CPP World
```


### ruby {#ruby}

```ruby
puts "Hello Ruby World!"
```

```text
Hello Ruby World!
```


### python {#python}

```python
print("Hello Python World!")
```

```text
Hello Python World!
```


### haskell {#haskell}

```haskell
putStrLn "Hello Haskell World!"
```

```text
Hello Haskell World!
```


### yaml {#yaml}

```yaml
test:
  a:
    - 1
    - 2
  b:
    - 3
    - 4
```


### elisp {#elisp}

```elisp
(print "Hello EmacsLisp World!")
```

```text

"Hello EmacsLisp World!"
```


## 其它 {#其它}


### 文档格式转换工具 pandoc {#文档格式转换工具-pandoc}


### 检查 org 文档格式 {#检查-org-文档格式}

使用 `org-lint` 检查
