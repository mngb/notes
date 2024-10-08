+++
title = "email"
author = ["PENG Kevin"]
description = "emails"
keywords = ["email"]
tags = ["email"]
draft = false
+++

## setup {#setup}

download email tool
: `apt-get install offlineimap`

index email tool
: apt-get install mu


## config in [emacs]({{< relref "emacs.md" >}}) {#config-in-emacs--emacs-dot-md}

send email behind socks5 proxy tool
: apt-get install msmtp


## configure {#configure}

1.  copy files
    <../email/.offlineimaprc>
    <../email/.offlineimap.py>
    <../email/.authinfo.gpg>
    to
    <~/>
2.  configure emacs variables in
    [mu4e]({{< relref "emacs_init#mu4e" >}})
3.  configure msmtp variables in
    [msmtp](/home/pk/workspace/rdf/rdf/redef/repos/rdf-mix/email/.msmtprc)


## run {#run}

First time, goto `~/` which contain configure files and run
`offlineimap`, then
For old mu try:
`mu index --maildir=<config_mail_dir_in_.py>`
For new mu (1.10.8 verified):

```bash
mu init --maildir=<config_mail_dir_in_.py>
mu index
```

For 163 email, offlineimap need &gt;7.7.3
offlineimap 有时会卡住，换了 isync ，但是不支持 proxy sock5。
卡住的问题可能是 proxy 的问题？？重启下 offlineimap 就顺畅了。


## write email {#write-email}

use `org-mime` package,

```emacs-lisp
;; email buffer to html
(org-mime-htmlize)

;; edit email in org-mode buffer
(org-mime-edit-mail-in-org-mode)

;; convert a org buffer to html
(org-mime-org-buffer-htmlize)

;; convert a org heading to html
(org-mime-org-subtree-htmlize)
(mu4e-compose-mode) ; enter email send mode
```


### 插入图片 {#插入图片}

用插入链接命令, 类型为 `file`, 不能有 `description`
