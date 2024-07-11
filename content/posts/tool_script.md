+++
title = "tool-script"
author = ["PENG Kevin"]
draft = false
+++

## gen_bookmark {#gen-bookmark}

1.  打开 emacs terminal, cd 到 tool-script 目录
2.  准备好 pdf 文件，一般放到 </home/pk/samba_share/pdf/>
3.  运行
    1.  ocr 提取目录内容
        ```bash
        ./gen_bookmark.sh <pdf_file_path> <start_content_page> <end_content_page> <content_column_num>
        ```
    2.  手动修改生成的 `<>_bookmark_all.txt` 文件，修改识别错误的页面，多余的文字
        等
    3.  生成 `<>_bookmark_all.yml` 文件
        ```bash
        ./gen_bookmark.sh <pdf_file_path> <start_page1_offset>
        ```
        手动修改该文件，形成树形书签。
    4.  添加书签到 pdf 文件
        ```bash
        ./gen_bookmark.sh <pdf_file_path>
        ```
