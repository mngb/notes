+++
title = "emacs_keymap"
author = ["PENG Kui"]
tags = ["keymap", "emacs"]
draft = false
+++

## 按键分配原则 {#按键分配原则}

-   将按键绑定按击键次数分类, hit1, hit2, hit3。大于三次不使用。
-   -   **连续键(continuous key):** 如所有 hit1 和 [M-&lt;key&gt;]+ 或 [C-&lt;key&gt;]+, 可
        支持连续不间断按，一般用于某些命令使用时一般连续使用
    -   **断续键(discrete key):** 命令使用时一般两个该命令间是断续的, 如 `C-x j`,
        手部动作是：

        1.  按下 C-x
        2.  松开 C 键
        3.  等待片刻，按下 j

        相比连续键，多一个松开 C/M 键的步骤
-   考虑按键位置、击键次数、按键含义等，越大越舒适
    -   **舒适性排序:** 1.  &lt;char&gt; &gt; C-&lt;char&gt; &gt; M-&lt;char&gt; ,
        2.  hit1 &gt; hit2 &gt; hit3
        3.  continuous key &gt; discrete key
        4.  M-&lt;右手char&gt; &gt; M-&lt;左手char&gt;
    -   &lt;char&gt;舒适等级表
        ![](/ox-hugo/key_layout.jpg)


## 按键分配地图 {#按键分配地图}

-   \* 表示该按键已默认分配，不可再使用或重定义
-   ? 表示可用来自定义, 建议定义成命令，不建议定义成 map 前缀键
-   - 表示可用来自定义, 建议定义成 map 前缀键

<a id="table--hit1 绑定定义"></a>

| &lt;char&gt; | C-&lt;char&gt;              | M-&lt;char&gt;              | comfort |
|--------------|-----------------------------|-----------------------------|---------|
| a            | \* beginning-of-line        | - rdf-org                   | 100     |
| b            | \* back-char                | - rdf-bookmark              | 90      |
| c            | \* &lt;reserved-prefix&gt;  | - rdf-clang-development     | 90      |
| d            | \* delete-char              | - rdf-desktop               | 95      |
| e            | \* end-of-line              | - rdf-eyebrowse             | 90      |
| f            | \* forward-char             | - rdf-flycheck-lang-tool    | 92      |
| g            | \* &lt;cancel&gt;           | -                           | 85      |
| h            | \* &lt;help-prefix&gt;      | - rdf-high-cost             | 85      |
| i            | \* &lt;tab&gt;              | - rdf-interactive           | 90      |
| j            | - set-mark-command          | - rdf-projectile            | 90      |
| k            | \* kill-line                | - rdf-haskell               | 95      |
| l            | \* recenter-top-bottom      | - rdf-low-cost              | 100     |
| m            | \* &lt;RET&gt;              | - rdf-email                 | 90      |
| n            | \* next-line                | \* rdf-next-window          | 95      |
| o            | dabbrev-expand              | \* rdf-jump-to-other-window | 100     |
| p            | \* previous-line            | \* rdf-previous-window      | 100     |
| q            | - quoted-insert             | - rdf-daily-Quality         | 95      |
| r            | undo-tree-redo              | - rdf-ruby                  | 85      |
| s            | swiper                      | - rdf-snippet               | 100     |
| t            | - rdf-define-jump           | - rdf-rust                  | 85      |
| u            | undo-tree-undo              | -                           | 85      |
| v            | \* scroll-up-command        | -                           | 85      |
| w            | \* backward-kill-word       | - rdf-web-commands          | 90      |
| x            | \* &lt;reserved-prefix&gt;  | - rdf-python-commands       | 95      |
| y            | \* &lt;yank&gt;             | - yank-pop                  | 85      |
| z            | \* scroll-down-command      | -                           | 95      |
| ;            | \* rdf-backward-global-mark |                             | 80      |
| ,            | \* rdf-forward-global-mark  |                             | 75      |
| .            |                             |                             | 70      |
| [            |                             |                             | 70      |
| ]            |                             |                             | 70      |

<a id="table--hit2 绑定定义 C-x 连续键"></a>

| &lt;char1&gt; | &lt;char2&gt; | Command             | comfort |
|---------------|---------------|---------------------|---------|
| C-x           | C-a           |                     |         |
| C-x           | C-b           |                     |         |
| C-x           | C-c           | copy-region-as-kill |         |
| C-x           | C-d           | delete-frame        |         |
| C-x           | C-e           |                     |         |
| C-x           | C-f           |                     |         |
| C-x           | C-g           |                     |         |
| C-x           | C-h           |                     |         |
| C-x           | C-i           |                     |         |
| C-x           | C-j           |                     |         |
| C-x           | C-k           | kill-current-buffer |         |
| C-x           | C-l           |                     |         |
| C-x           | C-m           |                     |         |
| C-x           | C-n           | recursive-edit      |         |
| C-x           | C-o           |                     |         |
| C-x           | C-p           | exit-recursive-edit |         |
| C-x           | C-q           |                     |         |
| C-x           | C-r           |                     |         |
| C-x           | C-s           | \* save-buffer      |         |
| C-x           | C-t           |                     |         |
| C-x           | C-u           |                     |         |
| C-x           | C-v           |                     |         |
| C-x           | C-w           | kill-region         |         |
| C-x           | C-x           |                     |         |
| C-x           | C-y           |                     |         |
| C-x           | C-z           |                     |         |

<a id="table--hit2 绑定定义 C-x 断续键"></a>

| &lt;char1&gt; | &lt;char2&gt; | Command                  | comfort |
|---------------|---------------|--------------------------|---------|
| C-x           | a             |                          |         |
| C-x           | b             | switch-to-buffer         |         |
| C-x           | c             |                          |         |
| C-x           | d             |                          |         |
| C-x           | e             |                          |         |
| C-x           | f             |                          |         |
| C-x           | g             |                          |         |
| C-x           | h             |                          |         |
| C-x           | i             |                          |         |
| C-x           | j             |                          |         |
| C-x           | k             |                          |         |
| C-x           | l             | goto-line                |         |
| C-x           | m             |                          |         |
| C-x           | n             |                          |         |
| C-x           | o             |                          |         |
| C-x           | p             |                          |         |
| C-x           | q             | query-replace-regexp     |         |
| C-x           | r             |                          |         |
| C-x           | s             | isearch-forward-regexp   |         |
| C-x           | t             |                          |         |
| C-x           | u             |                          |         |
| C-x           | v             |                          |         |
| C-x           | w             |                          |         |
| C-x           | x             |                          |         |
| C-x           | y             |                          |         |
| C-x           | z             |                          |         |
| C-x           | ;             | execute-extended-command |         |
| C-x           | ,             | eval-expression          |         |
|               |               |                          |         |

<a id="table--hit2 绑定定义 C-c 连续键"></a>

| &lt;char1&gt; | &lt;char2&gt; | Command | comfort |
|---------------|---------------|---------|---------|
| C-c           | C-a           |         |         |
| C-c           | C-b           |         |         |
| C-c           | C-c           |         |         |
| C-c           | C-d           |         |         |
| C-c           | C-e           |         |         |
| C-c           | C-f           |         |         |
| C-c           | C-g           |         |         |
| C-c           | C-h           |         |         |
| C-c           | C-i           |         |         |
| C-c           | C-j           |         |         |
| C-c           | C-k           |         |         |
| C-c           | C-l           |         |         |
| C-c           | C-m           |         |         |
| C-c           | C-n           |         |         |
| C-c           | C-o           |         |         |
| C-c           | C-p           |         |         |
| C-c           | C-q           |         |         |
| C-c           | C-r           |         |         |
| C-c           | C-s           |         |         |
| C-c           | C-t           |         |         |
| C-c           | C-u           |         |         |
| C-c           | C-v           |         |         |
| C-c           | C-w           |         |         |
| C-c           | C-x           |         |         |
| C-c           | C-y           |         |         |
| C-c           | C-z           |         |         |
