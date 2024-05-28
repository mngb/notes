+++
title = "pdf-ocr"
author = ["PENG Kui"]
draft = false
+++

A:PROPERTIES:
:ID:       91c44778-d4d8-4f9b-97c9-27963d7aaed3

:END:


## pdf split and merge {#pdf-split-and-merge}

use `poppler-utils`
`pdfseparate`
`pdfunite`


## convert pdf to picture {#convert-pdf-to-picture}

use `convert`


## pdf ocr {#pdf-ocr}

用 python3 的 `CnOcr` 库。
不用 `paddle` 库，太难装。


## add pdf bookmark {#add-pdf-bookmark}

用 python3 的 `pypdf2` 库。
不用 ruby 的 `prawn-template` 库，有些文件会产生空白文件。
