+++
title = "haml"
author = ["PENG Kui"]
tags = ["template", "rails", "haml"]
draft = false
+++

## 基本格式 {#基本格式}

```haml
!!!5
%tag#id.class(attr1="a", attr2="b")
  contents
  -# haml 注释
  -# - 代替 ERB 的 <% %>
  -# = 代替 ERB 的 <%= %>
  /
    html 注释

-# 相当于 <div id="id2"> </div>
#id2
  -# #{} 间插入的是 ruby 代码计算结果
  #id3.class(attr1="#{1+1}")
```


## 参考链接 {#参考链接}

<https://github.com/haml/haml>
