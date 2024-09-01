+++
title = "projectile"
author = ["PENG Kevin"]
draft = false
+++

## projectile 项目识别过程 {#projectile-项目识别过程}


### 关键变量 {#关键变量}

projectile-project-root-functions
: 定义项目的识别函数表，是一个列表，元素是项目识别函数，
    依次调用，最先识别项目的函数先返回，后续识别函数将不被调用。
    默认的识别函数及其行为依次为：
    1.  projectile-root-local
        在目录的 .dir-locals.el 中设置目录局部变量
        `projectile-project-root` ，这个函数直接返回这个变量作为项目识别结果。
    2.  projectile-root-marked
        调用 projectile-root-bottom-up 识别最先找到有 `.projectile` 文件的目录。
    3.  projectile-root-bottom-up
        调用 projectile-root-bottom-up 识别最先找到列表变量
        `projectile-project-root-files-bottom-up` 中某一个文件(依次)的目录。
    4.  projectile-root-top-down
        找到所有父级目录中包含列表变量中 `projectile-project-root-files` 文件的
        目录，返回离当前目录最远的。el 代码没看懂，
        但是经过测试，其行为和 projectile-root-bottom-up 一样的？？？
    5.  projectile-root-top-down-recurring
