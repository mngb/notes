+++
title = "latex"
author = ["PENG Kui"]
draft = false
+++

## inline preview {#inline-preview}

use `org-latex-preview` command,
use \\(x^2 + y^2 = z^2\\) to edit latex formula


## 公式编辑常用符号 {#公式编辑常用符号}

-   \\(\int\_{0}^{\infty}\\)
-   \\(\frac{a}{b}\\)
-   \\(\dot{x},\ddot{x},\dddot{x}\\)


## tips {#tips}


### 导出中文不显示的问题 {#导出中文不显示的问题}

在导出的 tex 文件中加上 `\usepackage{ctex}`,
再用 `xelatex` 编译。
