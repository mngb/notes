+++
title = "jekylly"
author = ["PENG Kevin"]
draft = false
+++

## 常用操作 {#常用操作}


### 新建空项目 {#新建空项目}

`bundle exec jekyll new <prj_name> --blank`


### 编译包含草稿目录 {#编译包含草稿目录}

`bundle exec jekyll build --drafts`


### 启动时含有草稿目录 {#启动时含有草稿目录}

`bundle exec jekyll serve --drafts`


### 启动服务 {#启动服务}

`bundle exec jekyll serve`


### 更换主题 {#更换主题}


### 安装插件 {#安装插件}


## 部署 {#部署}


### github {#github}

1.  github -&gt; setting -&gt; pages
2.  修改 Gemfile 文件，按照注释内容修改，
    打开 `gem "github-pages"` ,
    注释掉 `gem "jekyll"`
3.  push 到 github (注意 assets 目录需要提交，\__site 目录不必提交), 自动执行 action 后，在
    deploy 的输出会看到 public 页面链接。
