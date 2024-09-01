+++
title = "python"
author = ["PENG Kevin"]
draft = false
+++

## coding style {#coding-style}

-   [python style]({{< relref "python_style.md" >}})


## language {#language}

循环

```python
import sys

dict_demo = {}

for k,v in dict_demo.items():
    print(f"{k}={v}")

x = [ x*x for x in [1,2,3]]
```

命令行参数

```python
import sys
img_fp = sys.argv[1]
```

逻辑运算

```python
True and True
not True
True or False
```

字符串处理

```python
x = 1
"x = %d" % x
f"x = {x}"
```

文件处理

```python
import os
os.path.exists("/home/pk")
```


## library {#library}


### pip {#pip}

`pip install <pkg_name> -i https://pypi.tuna.tsinghua.edu.cn/simple`
`pip freeze > requirements.txt` 导出当前安装的包


### qt {#qt}

`pyside2`


### data process {#data-process}

`matplotlib pandas scipy opencv-python`


### common use {#common-use}

`python-language-server pytest`


### elpy {#elpy}

`rope jedi importmagic autopep8 flake8`


### bluetooth {#bluetooth}

`pybluez`


### opengl {#opengl}

`pyopengl`


### install lsp-server {#install-lsp-server}

`pip install python-lsp-server`
