+++
title = "blog"
author = ["PENG Kui"]
tags = ["blog"]
draft = false
+++

## Notes Release Steps {#notes-release-steps}

1.  edit notes node with `org-roam` in emacs
2.  run `rdf-export-roam-to-hugo`, will generate md files
3.  run `python3 dump_roam_db.py`, generate json file for d3js
4.  copy json file to site directory for d3js use


## Blog Release Steps {#blog-release-steps}

1.  使用 `org-mode` 编写 Blog
2.  使用自定义导出项目 `org-blog` , 将 `org` 文件导出为带有 `jekyll` 头的 `html` 文件
3.  执行 `jekyll build`, 将 `_posts` 下 `html` 文件按规则挪到 `_site` 目录下
4.  执行 `git commit`, 提交 `_site` 目录
5.  `github pages` 将自动运行 actions, 执行远端 Pages 构建
