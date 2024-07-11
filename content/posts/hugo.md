+++
title = "hugo"
author = ["PENG Kevin"]
tags = ["hugo"]
draft = false
+++

## how to {#how-to}

install
: `sudo apt-get install hugo`

start
: 1.  `hugo new site <site_name>`
    2.  Add theme (`cd themes; git clone <theme-repo>`)
    3.  Add md file `hugo new posts/<x.md>`
    4.  Start server `hugo server -D`


## Github 上搭建基于 Hugo 的个人笔记网站 {#github-上搭建基于-hugo-的个人笔记网站}


### 使用 org-roam 记录笔记 {#使用-org-roam-记录笔记}

按前缀键 `M-a` 查看具体命令


### 使用 ox-hugo 导出 org-roam 笔记 {#使用-ox-hugo-导出-org-roam-笔记}

参见命令 `rdf-export-roam-to-hugo` 。


### 提交到 Github {#提交到-github}


#### 仓库的划分 {#仓库的划分}

1.  静态文件仓库，必需命名为 `ox-hugo` , 因 `ox-hugo` 包导出依赖的图片，文件时，
    默认生成目录为 `ox-hugo` , 而导出的 `hugo` 笔记内容对依赖图片，文件的链接采
    用了基于 `host` 根 `url` 的方式访问，与 `github` `pages` 服务方式不兼容，因此将
    静态文件独立出来，并基于 `Github Pages` 创建 `静态页面` 网站（不基于 hugo,
    jekyll）。
2.  `Hugo` 项目仓库。由 `hugo new site` 生成，=ox-hugo= 导出内容会生成到该项目中。
    该仓库基于 `Github Pages` 创建 `Hugo 页面服务`


## FAQ {#faq}


### can't evaluate field Build in type string {#can-t-evaluate-field-build-in-type-string}

update hugo to latest version
