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


#### 安装主题 {#安装主题}

1.  修改 `Gemfile` 文件，添加主题对应的 `gem`, 并执行 `bundle` 安装
2.  执行 `gem info <theme-gem-name>` 查看安装位置
3.  将主题 `gem` 安装位置对应内容拷贝到当前项目
4.  在 `_config.yml` 文件中对主题进行配置


#### minimal-mistakes-jekyll 主题主要配置项 {#minimal-mistakes-jekyll-主题主要配置项}

search
: 是否启动搜索

read_time
: 是否显示预估的博客阅读时长

show_date
: 是否显示博客创建日期

author_profile
: 是否显示该篇博客作者信息页


### 安装插件 {#安装插件}


## 部署 {#部署}


### github {#github}

1.  github -&gt; setting -&gt; pages
2.  修改 Gemfile 文件，按照注释内容修改，
    打开 `gem "github-pages"` ,
    注释掉 `gem "jekyll"`
3.  push 到 github (注意 assets 目录需要提交，\__site 目录不必提交), 自动执行 action 后，在
    deploy 的输出会看到 public 页面链接。


### org-mode 中文档编写注意事项 {#org-mode-中文档编写注意事项}

不要有 `{{` 前缀，会被解释成 liqui 格式语法文件。
