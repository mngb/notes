+++
title = "doc-zh style"
author = ["PENG Kui"]
draft = false
+++

## 5W {#5w}

-   WHO 写给自己看
-   WHAT 记录知识点，方便自己后续能快速回忆使用
-   WHEN 需要记录如软件，模块的版本等变量
-   WHERE R-sys 相对位置或获取代码
-   WHY 积累知识，产生内容


## 一般结构 {#一般结构}


### 格式和规范 {#格式和规范}

中文文档规范参考列表
: -   <https://github.com/ruanyf/document-style-guide>
    -


#### 文本间距 {#文本间距}

1.  中英文字符间有空格
2.  英文字符和中文标点间无空格
3.  单位和英文字符间留出空白


#### 句子风格 {#句子风格}

1.  避免使用长句，不要多于40个字
2.  使用简单句和并列句，避免使用复合句
3.  尽量用肯定，主动语态，避免使用双重否定，被动语态
4.  代词指代内容必需明确


#### 标点 {#标点}

1.  英文句子使用英文标点，中文使用英文标点
2.  中文书籍名用《》替换


### 文档组织 {#文档组织}

1 开头 coding, title, keywords, ... 等，使用笔记模板
2 目录，体现文档整体结构和快速跳转


## 相关工具 {#相关工具}


### 文档编写 {#文档编写}

使用 org-mode 编写。


### 图片处理 {#图片处理}

-   tool
-   标注
-   缩放
-   生成
-   格式转化 ffmpeg


### 截屏和录屏 {#截屏和录屏}

linux 下使用 `kazam` 可录制成 mp4 格式，
使用 `byzanz` 可录制 gif 格式，
使用 `mplayer` 回放视频格式，
使用 `ffmpeg` 进行图片、视频格式转换，
按键录制使用 emacs 的 `keycast` 录制。

```bash
# 1. kazam
# start kazam GUI
kazam

# 2. byzanz
# check screen pixel
xdpyinfo | grep dimensions
byzanz-record -d 30 --delay=5 -x 0 -y 0 -w 1920 -h 1080 x.gif

```


### 表格 {#表格}


### 框图 {#框图}

-   plantuml
-   draw.io


### REPL 环境 {#repl-环境}

-   TODO


### 排版和美化 {#排版和美化}

-   CSS
