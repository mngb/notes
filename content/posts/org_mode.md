+++
title = "org-mode"
author = ["PENG Kui"]
draft = false
+++

## navigation {#navigation}

-   `C-c C-n` org-next-visible-heading
-   `C-c C-p` org-previous-visible-heading
-   `C-c C-f` org-forward-heading-same-level
-   `C-c C-b` org-backward-heading-same-level
-   `C-c C-u` outline-up-heading
-   `C-c C-j` org-goto


## edit {#edit}

-   `M-RET` org-meta-return, 直接回车，当前在 head 和 content 中间时，会将
    content 后移
-   `C-RET` org-insert-heading-respect-content, 插入 head 时会考虑当前 head 的
    内容块
-   `TAB`
-   `C-c C-l` 插入链接，插入图片不要用此命令，用 `snippet` 的 `img`


## org-style {#org-style}

[org style]({{< relref "org_style.md" >}})
