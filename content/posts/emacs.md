+++
title = "emacs"
author = ["PENG Kevin"]
tags = ["emacs"]
draft = false
+++

## Emacs 手册 {#emacs-手册}

emacs
: [emacs.pdf](/ox-hugo/emacs.pdf)

elisp
: [elisp.pdf](/ox-hugo/elisp.pdf)


## Emacs 配置 {#emacs-配置}

-   环境初始化 [rdf system]({{< relref "rdf_system.md" >}})
-   配置文件 [emacs_init]({{< relref "emacs_init.md" >}})
-   按键地图 [emacs_keymap]({{< relref "emacs_keymap.md" >}})


## 常用模式 {#常用模式}

-   [org-mode]({{< relref "org_mode.md" >}})
-   [org-roam]({{< relref "roam.md" >}})
-   自动补全 company-mode
-   代码导航 lsp-mode
-   交互 helm-mode


## Tips {#tips}


### mode-line {#mode-line}

-   configure use `mode-line-format`
-   debug use `format-mode-line`


### super-rights {#super-rights}

`C-x C-f` and type `/sudo::<filename>`


### get image size {#get-image-size}

`(image-size (image-get-display-property) :pixels)`


### Failed to verify signature archive-contents.sig {#failed-to-verify-signature-archive-contents-dot-sig}

1.  `M-x set-variable RET package-check-signatures RET nil`
2.  `M-x package-refresh-contents`
3.  install `gnu-elpa-keyring-updated` package


### imenu {#imenu}

查找定义，找不到定义时，可以启用 lsp-mode


### occur {#occur}

单个文件内查找行


### rgrep {#rgrep}

多个文件内查找行
