+++
title = "email"
author = ["PENG Kui"]
description = "emails"
keywords = ["email"]
tags = ["email"]
draft = false
+++

## setup {#setup}

download email
: apt-get install offlineimap

index email
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
3.  configure msmtp variables in


## run {#run}

First time, goto `~/` which contain configure files and run
`offlineimap`, then `mu index --maildir=<config_mail_dir_in_.py>`
For 163 email, offlineimap need &gt;7.7.3


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
