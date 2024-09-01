+++
title = "latex"
author = ["PENG Kevin"]
draft = false
+++

## inline preview {#inline-preview}

use `org-latex-preview` command,
use <img src="/ltximg/latex_4f339647912db8015cabd74cb735bc958ed37418.png" alt="$x^2 + y^2 = z^2$" /> to edit latex formula


## 公式编辑常用符号 {#公式编辑常用符号}

-   <img src="/ltximg/latex_c8c89f23afd2d7aed22093560d1c15b8e77eb962.png" alt="$\int_{0}^{\infty}$" />
-   <img src="/ltximg/latex_4b04708cb4f7da034256806b39ef57f4da5d4d40.png" alt="$\frac{a}{b}$" />
-   <img src="/ltximg/latex_987116da94df5e62531cc2457596ab27ebc3298f.png" alt="$\dot{x},\ddot{x},\dddot{x}$" />


## tips {#tips}


### 导出中文不显示的问题 {#导出中文不显示的问题}

在导出的 tex 文件中加上 `\usepackage{ctex}`,
再用 `xelatex` 编译。
