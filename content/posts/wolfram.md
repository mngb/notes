+++
title = "*wolfram"
author = ["PENG Kevin"]
draft = false
+++

## init {#init}

run `wolframscript` to start


## jupyter {#jupyter}

use <https://gitee.com/pkui/wolfram-language-for-jupyter_pk>
emacs fornt-end use ein <https://github.com/millejoh/emacs-ipython-notebook>
work with org mode <https://github.com/millejoh/emacs-ipython-notebook/blob/master/README.rst#ob-ein>


## mathmatic {#mathmatic}

program <https://www.wolfram.com/language/fast-introduction-for-programmers/zh/>

% last result
= natrue language input
InputForm[] show structure of expression
Module 使用词法作用域（局部化名称）.
Block 使用动态作用域（局部化值）.
DynamicModule 使用文档中的作用域.
Sow/Reap 和 Throw/Catch 是过程式编程中传递数据和控制的有用方式

Numeric:
使用 N（可能更快）获取数值结果
用 \` 以数值明确指明精度
矩阵是列表的列表
对于复数，I
SparseArray 给出稀疏数组


## examples {#examples}

failure to integrate with org-mode, following
<http://xahlee.info/emacs/misc/xah-wolfram-mode.html>

<a id="code-snippet--9316315f-25bb-490b-8738-17e51d12ab79"></a>
```ein-wolframlanguage12
p=Plot[Sin[x], {x, 0, 6 Pi},Frame->True];
Export["images/sine.png",p];
Print["images/sine.png"]
```


## language {#language}


### comment {#comment}

(\* \*)


### Help {#help}

Names
Information/?


### Others {#others}

Function[ {x,y}, x + y ]
Function[ #1 + #2 ]
(#1 + #2)&amp;
Sym::usage = "docstring..."


### Functions {#functions}


#### Symbol {#symbol}


#### Matrix {#matrix}
