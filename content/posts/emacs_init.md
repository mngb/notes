+++
title = "emacs_init"
author = ["PENG Kevin"]
draft = false
+++

## how to configure {#how-to-configure}

-   use command `C-c '` to edit elisp with elisp-mode
-   remove "#+PROPERTY: header-args :tangle "~/_redef-emacs.el"
    this will always write file to :tangle, make start up slowly.
    Use default, will not write if org file has no change.
-   -   add 'vm.swappiness = 1' to '/etc/sysctl.conf' and exec `sysctl -p`


## content make sure in .emacs <span class="tag"><span class="init">init</span></span> {#content-make-sure-in-dot-emacs}

```emacs-lisp
;; (setq gc-cons-threshold 50000000) ;; this can fast emacs startup time
;; (setq rdf-emacs-init-file (getenv "emacs_init_file"))
;; (setq rdf-emacs-local-mepa-dir (getenv "emacs_local_mepa"))
;; (setq rdf-emacs-org-template-dir
;;       (concat (file-name-directory rdf-emacs-init-file)
;;          "../notes/org_templates/"))
;; (package-initialize)
;; (eval-when-compile
;;   (if (>= emacs-major-version 27)
;;       (require 'cl-lib)
;;     (require 'cl))
;;   (if (featurep 'use-package)
;;       (require 'use-package)
;;     (require 'ext-use-package (expand-file-name "~/.emacs.d/ext/use-package/ext-use-package.el"))))
;; (use-package org)
;; (org-babel-load-file rdf-emacs-init-file)
;; (setq gc-cons-threshold 10000000)
```


## all required ext package list <span class="tag"><span class="ext_list">ext-list</span></span> {#all-required-ext-package-list}

```emacs-lisp
;; non-melpa packages
(setq rdf-ext-non-melpa-package-list
      (list
       'bookmark-plus ;;
       'frame ;;
       'dired+))
;; melpa packages
(setq rdf-ext-melpa-package-list
      (list
       ;; melpa
       'use-package
       'elpa-mirror
       'esup

       ;; daily
       'guide-key
       'keyfreq
       'undo-tree
       'company
       'google-translate
       'org-super-agenda

       ;; ruby
       'yaml-mode
       'inf-ruby
       'rubocop
       'robe
       'enh-ruby-mode

       ;; haskell
       'haskell-mode
       'lsp-haskell

       ;; version control
       'magit
       'transient

       ;; project manage
       'projectile
       'ggtags

       ;; smart
       'helm
       'helm-projectile
       'async
       'helm-ag
       'helm-gtags
       'swiper
       'swiper-helm
       ;;'counsel contained in swiper
       'counsel-projectile
       ;;; 'dumb-jump ; too slowly deplicate
       'ace-window
       'avy
       'visual-regexp
       'eyebrowse
       'ivy
       'multiple-cursors
       'yasnippet
       'yasnippet-classic-snippets
       'graphviz-dot-mode
       'beacon

       ;; funning
       'emms
       'desktop+
       'wttrin

       ;; web-dev
       ;;
       'js2-mode
       'web-mode
       'impatient-mode
       'skewer-mode
       'ghub
       'markdown-mode
       'indium

       ;; style
       'organic-green-theme
       'xterm-color

       ;; email
       'org-mime
       'bbdb
       'bbdb-vcard

       ;; rss
       'elfeed
       'elfeed-org
       ))
```


## redef customize <span class="tag"><span class="redef">redef</span></span> {#redef-customize}


### redef environments setup                                             :env:<span class="org-target" id="org-target--custom"></span> {#redef-environments-setup-env}

```emacs-lisp
(use-package redef-boot
  :load-path "~/.emacs.d/redef/boot/")
(use-package os-wrapper
  :after redef-boot
  :load-path "~/.emacs.d/redef/lib/"
  :config
  (r-os-wrapper-config))
(use-package redef-lib
  :requires (os-wrapper)
  :load-path "~/.emacs.d/redef/lib/")
(use-package redef-config
  :requires (redef-lib)
  :load-path "~/.emacs.d/redef/"
  :after (redef-lib)
  :init
  ;;(prefer-coding-system 'utf-8)
  (r-os-coding-config)
  (setq ext-helm-mode-used (string-equal (r-get-then-del-env "emacs_use_helm") "yes")) ;; commonly used variable
  (setq ext-proxy-used (string-equal (r-get-then-del-env "emacs_use_proxy") "yes"))
  (setq ext-company-clang-executable (r-get-then-del-env "company_clang_executable"))
  (setq ext-emms-music-dir (r-get-then-del-env "emms_music_dir"))
  (setq ext-git-executable-program (r-get-then-del-env "git_executable_program"))
  (setq ext-gpg-program (r-get-then-del-env "gpg_program"))
  (setq ext-asy-bin-dir (r-get-then-del-env "asy_bin_dir"))
  (setq ext-dot-program (r-get-then-del-env "dot_program"))
  (setq ext-ruby-program (r-get-then-del-env "ruby_program"))
  (setq ext-root-program (getenv "R_PROGRAMS_DIR"))
  (setq ext-root-workspace (getenv "R_WORKSPACE_DIR"))
  (setq ext-tmp-dir (concat rdf_email "/../tmp/"))
  (setq calc-gnuplot-name (r-get-then-del-env "gnuplot_program"))
  (setq ext-emailrelay-program (r-get-then-del-env "emailrelay_program"))
  (setq ext-emailrelay-cfg-dir (r-get-then-del-env "emailrelay_cfg_dir"))
  (setq ext-chrome-program (r-get-then-del-env "chrome_program"))
  (setq ext-nodejs-dir (r-get-then-del-env "nodejs_program"))
  (setq ext-langtool-program (r-get-then-del-env "langtool_program"))
  (setq ext-plantuml-program (r-get-then-del-env "plantuml_program"))
  (setq ext-markdown-program (r-get-then-del-env "markdown_program"))
  (setq ext-vpn-program (r-get-then-del-env "vpn_program"))
  (setq ext-vpn-program2 (r-get-then-del-env "vpn_program2"))
  (setq ext-haskell-stack-program (r-get-then-del-env "haskell_stack_program"))
  (setq ext-haskell-engine-program (r-get-then-del-env "haskell_hie_program"))
  (setq ext-emacs-source-dir (r-get-then-del-env "emacs_source_dir"))
  (setq ext-mingw-gcc-program (r-get-then-del-env "mingw_gcc_program"))
  (setq ext-telegram-gui (r-get-then-del-env "telegram_program"))
  (setq ext-rtags-path (r-get-then-del-env "rtags_program"))
  (when ext-rtags-path
    (setq ext-rtags-path (file-name-directory ext-rtags-path)))
  (setq rdf-emacs-org-template-dir
        (concat (file-name-directory rdf-emacs-init-file)
                "../notes/org_templates/"))
  (if ext-nodejs-dir (setq ext-nodejs-dir (file-name-directory ext-nodejs-dir)))
  ;; grep and find for rgrep command
  (with-windows-nt
    (setq grep-program "rg")
    (setq find-program (concat (file-name-directory ext-git-executable-program) "../usr/bin/find.exe"))
   (setq shell-file-name (r-get-then-del-env "shell_file")))
  (define-prefix-command 'redef-global-key-bindings-low-effort-map)
  (define-prefix-command 'redef-global-key-bindings-high-effort-map)
  (define-prefix-command 'redef-global-key-bindings-interactive-map)
  (define-prefix-command 'redef-global-key-bindings-gtags-map)
  (define-prefix-command 'redef-global-key-bindings-projectile-map)
  (define-prefix-command 'redef-global-key-bindings-desktop-map)
  (define-prefix-command 'redef-global-key-bindings-emms-map)
  (define-prefix-command 'redef-global-key-bindings-snippet-map)
  (define-prefix-command 'redef-global-key-bindings-ruby-map)
  (define-prefix-command 'redef-global-key-bindings-python-map)
  (define-prefix-command 'redef-global-key-bindings-eyebrowse-map)
  (define-prefix-command 'redef-global-key-bindings-bookmark-map)
  (define-prefix-command 'redef-global-key-bindings-web-map)
  (define-prefix-command 'redef-global-key-bindings-org-agenda-map)
  (define-prefix-command 'redef-global-key-bindings-flycheck-map)
  (define-prefix-command 'redef-global-key-bindings-haskell-map)
  (define-prefix-command 'redef-global-key-bindings-mail-map)
  (define-prefix-command 'redef-global-key-bindings-clang-map)
  (define-prefix-command 'redef-global-key-bindings-rust-map)
  (define-prefix-command 'redef-global-key-bindings-sagemath-map)
  (defun r-start-vpn ()
    (interactive)
    (if (not ext-vpn-program)
        (message "ext-vpn-program not defined!")
      (async-shell-command ext-vpn-program)
      ;; =call r-auto-setup-proxy after vpn connected=
      ))
  (defun r-start-vpn2 ()
    (interactive)
    (if (not ext-vpn-program2)
        (message "ext-vpn-program2 not defined!")
      (async-shell-command ext-vpn-program2))
    ;; =call r-auto-setup-proxy after vpn connected=
    ;; select proxy by
    ;;    modify =~/.config/clash/config.yaml= "proxy-groups" field
    (with-linux
      (setq url-proxy-services
            '(("http" . "127.0.0.1:7890")
              ("https" . "127.0.0.1:7890")))
      (setenv "HTTP_PROXY" "http://127.0.0.1:7890")
      (setenv "HTTPS_PROXY" "http://127.0.0.1:7890"))
    )
  (defun r-jump-to-other-window ()
    (interactive)
         (if (> (count-windows) 3)
             (ace-window nil)
           (other-window 1)))
  (defun ext-skip-buffer-p (buffer-obj)
    (let ((skip-flag nil))
      (when buffer-obj
        (with-current-buffer buffer-obj
          (setq skip-flag
                (or (member (buffer-name)
                            '("*Messages*"
                              "*Help*" "*elfeed-log*"))
                    (eql major-mode 'helm-major-mode)
                    (string-match "^\\*emms.*\\*\\'" (buffer-name))
                    (string-match "^\\magit-\\w+:.*" (buffer-name))
                    ))))
      skip-flag))
  (defun ext-fetch-buffer (update-buffer)
    (let ((initial-buffer (current-buffer)) ; avoid inf loop
          (my-next-buffer (funcall update-buffer)))
      (while (and (ext-skip-buffer-p my-next-buffer)
                  (not (eql my-next-buffer initial-buffer)))
        (with-current-buffer (funcall update-buffer)
          (setq my-next-buffer (current-buffer))))))
  (defun redef-previous-buffer ()
    (interactive)
    (ext-fetch-buffer 'previous-buffer))
  (defun redef-next-buffer ()
    (interactive)
    (ext-fetch-buffer 'next-buffer))
  (defun everything-is-running ()
    "Check if Everything is running."
    (find "Everything.exe"
          (mapcar (lambda (p) (cdr (assoc 'comm (process-attributes p))))
                  (list-system-processes))
          :test 'string=))
  (defun r-start-everything ()
    (interactive) ;; linux use rlocate
    (let ((r-start-everything-background (lambda ()
                                           (start-process "everything-background" nil
                                                          "everything.exe" "-startup")))
          )
    (unless (everything-is-running)
      (async-start-process "everything-service" nil
                           (lambda () (funcall r-start-everything-background))
                           "everything.exe" "-install-service"))
    (funcall r-start-everything-background)))
  (defun r-find-func-dispatch (lsp-func helm-func)
    (cond
     ((and (boundp 'lsp-mode)
           (symbol-value 'lsp-mode))
      (if (called-interactively-p lsp-func)
          (call-interactively lsp-func)
        (funcall lsp-func)))
     ((and ext-helm-mode-used
           (functionp helm-func))
      (call-interactively helm-func))
     (t t))
    )
  (defun r-find-definition ()
    (interactive)
    (r-find-func-dispatch 'lsp-ui-peek-find-definitions
                          'helm-gtags-dwim))
  (defun r-find-reference ()
    (interactive)
    (r-find-func-dispatch 'lsp-ui-peek-find-references
                          'helm-gtags-find-rtag))
  (defun r-navi-stack-forward ()
    (interactive)
    (r-find-func-dispatch 'backward-forward-next-location
                          'backward-forward-next-location))
  (defun r-navi-stack-backward ()
    (interactive)
    (r-find-func-dispatch 'backward-forward-previous-location
                          'backward-forward-previous-location))
  (defun r-find-pop-stack ()
    (interactive)
    (r-find-func-dispatch 'xref-pop-marker-stack
                          'helm-gtags-pop-stack))
  (defun r-find-symbol ()
    (interactive)
    (r-find-func-dispatch 'lsp-ui-peek-find-workspace-symbol
                          'helm-gtags-find-pattern))
  (defun r-q-minor-mode ()
    (interactive)
    (message (format-mode-line 'minor-mode-alist)))

  (defun r-org-open-at-point-emacs ()
    (interactive)
    (org-open-at-point t))

  (defun r-redef-environment-setup ()
    (interactive)
    (shell-command (concat "sudo ldconfig " ext-root-program "/lib"))) ;; for clang environment

  ;; code reference:
  ;; https://stackoverflow.com/questions/3393834/how-to-move-forward-and-backward-in-emacs-mark-ring
  (defun marker-is-point-p (marker)
    "test if marker is current point"
    (and (eq (marker-buffer marker) (current-buffer))
         (= (marker-position marker) (point))))
  (defun push-mark-maybe ()
    "push mark onto `global-mark-ring' if mark head or tail is not current location"
    (if (not global-mark-ring) (error "global-mark-ring empty")
      (unless (or (marker-is-point-p (car global-mark-ring))
                  (marker-is-point-p (car (reverse global-mark-ring))))
        (push-mark))))
  (defun rdf-backward-global-mark ()
    "use `pop-global-mark', pushing current point if not on ring."
    (interactive)
    (push-mark-maybe)
    (when (marker-is-point-p (car global-mark-ring))
      (call-interactively 'pop-global-mark))
    (call-interactively 'pop-global-mark))
  (defun rdf-forward-global-mark ()
    "hack `pop-global-mark' to go in reverse, pushing current point if not on ring."
    (interactive)
    (push-mark-maybe)
    (setq global-mark-ring (nreverse global-mark-ring))
    (when (marker-is-point-p (car global-mark-ring))
      (call-interactively 'pop-global-mark))
    (call-interactively 'pop-global-mark)
    (setq global-mark-ring (nreverse global-mark-ring)))
  (defun rdf-get-select-region-char-num ()
    (interactive)
    (let ((mark (mark))
          (point (point)))
      (if mark
          (message "%d" (abs (- point mark)))
        (message "Mark not set!"))))

  (defun rdf-start-screen-record (file-name record-seconds)
    (interactive "sRecord File:\nnRecord Seconds: ")
    ;; (x-display-pixel-width)
    ;; (x-display-pixel-height)
    (let ((delay-seconds 5)
          (record-emacs-only t) ;; otherwise record fullscreen
          (frame-pos (frame-position))
          (tmp-buffer-name "*byzanz*")
          (record-file-name (concat rdf-wdir "/byzanz/" file-name ".gif")))
      (message "Record %s.gif(%d S) in %d S..." file-name record-seconds delay-seconds)
      (if record-emacs-only
          (async-shell-command (format "byzanz-record -d %d --delay=%d -x %d -y %d -w %d -h %d %s"
                                       record-seconds delay-seconds
                                       (car frame-pos) (cdr frame-pos)
                                       (frame-outer-width) (frame-outer-height)
                                       record-file-name)
                               tmp-buffer-name)
        (async-shell-command (format "byzanz-record -d %d --delay=%d -x 0 -y 0 -w %d -h %d %s"
                                     record-seconds delay-seconds
                                     (x-display-pixel-width) (x-display-pixel-height)
                                     record-file-name)
                             tmp-buffer-name))))
  (with-linux
   (add-hook 'after-init-hook 'r-start-vpn2))

  :bind-keymap* (("M-l" . redef-global-key-bindings-low-effort-map) ; low effort comand, cost little time to run
                 ("M-h" . redef-global-key-bindings-high-effort-map) ; hight effort command, cost many time to run
                 ("M-i" . redef-global-key-bindings-interactive-map)
                 ("C-t" . redef-global-key-bindings-gtags-map)
                 ("M-j" . redef-global-key-bindings-projectile-map)
                 ("C-c e" . redef-global-key-bindings-emms-map)
                 ("M-s" . redef-global-key-bindings-snippet-map)
                 ("M-r" . redef-global-key-bindings-ruby-map)
                 ("M-x" . redef-global-key-bindings-python-map)
                 ("M-e" . redef-global-key-bindings-eyebrowse-map)
                 ("M-w" . redef-global-key-bindings-web-map)
                 ("M-k" . redef-global-key-bindings-haskell-map)
                 ("M-a" . redef-global-key-bindings-org-agenda-map) ; agenda and some org command
                 ;; -k will kill some region some times
                 ("M-b" . redef-global-key-bindings-bookmark-map)
                 ("M-d" . redef-global-key-bindings-desktop-map)
                 ("M-f" . redef-global-key-bindings-flycheck-map)
                 ;; "M-q" for org-roam-dailies-map
                 ("M-m" . redef-global-key-bindings-mail-map) ; eMail and comMunication command
                 ("M-c" . redef-global-key-bindings-clang-map) ; cpp development
                 ("M-t" . redef-global-key-bindings-rust-map) ; rust development
                 ("M-g" . redef-global-key-bindings-sagemath-map)
                 )
  :bind (
         ;; in helm window, following bindings shall be override
         ("M-o" . r-jump-to-other-window)
         ("C-z" . scroll-down-command)
          )
  :bind* (
          ;;
          ;; emacs has no redo, do that by C-g then undo
          ;; if use undo-tree, redo has a special command
          ;; and emacs's redo seems unable to work
          ;;
          ("C-;" . rdf-backward-global-mark)
          ("C-'" . rdf-forward-global-mark)
          ("M-y" . yank-pop)
          ("C-u" . undo)
          ("M-p" . redef-previous-buffer)
          ("M-n" . redef-next-buffer)
          ("C-o" . dabbrev-expand)
          ("C-w" . backward-kill-word)
          ("C-x C-c" . copy-region-as-kill)
          ("C-x C-d" . delete-frame)
          ("C-x C-j" . set-mark-command)
          ("C-x C-k" . kill-current-buffer)
          ("C-x C-n" . recursive-edit)
          ("C-x C-o" . r-open-at-point-emacs)
          ("C-x C-p" . exit-recursive-edit)
          ("C-x C-w" . kill-region)
          ("C-x b" . switch-to-buffer)
          ("C-x l" . goto-line)
          ("C-x q" . query-replace-regexp)
          ("C-x s" . isearch-forward-regexp)
          ("C-x ;" . execute-extended-command)
          ("C-x ," . eval-expression)
          ("C-c C-o" . r-org-open-at-point-emacs)
          ("M-]" . (lambda () (interactive)
                     (cond
                      ((equalp major-mode 'ruby-mode) (ruby-forward-sexp))
                      ((equalp major-mode 'emacs-lisp-mode) (forward-sexp))
                      ((equalp major-mode 'c-mode) (c-forward-sexp))
                      (t t))))
          ("M-[" . (lambda () (interactive)
                     (cond
                      ((equalp major-mode 'ruby-mode) (ruby-backward-sexp))
                      ((equalp major-mode 'emacs-lisp-mode) (backward-sexp))
                      ((equalp major-mode 'c-mode) (c-backward-sexp))
                      (t t))))
          :map redef-global-key-bindings-low-effort-map
          ("j" . rectangle-mark-mode)
          ("o" . occur)
          ("p" . r-open-at-point-system)
          ("P" . proced) ;list system process
          ("R" . rgrep)
          ("i" . imenu)
          ("c" . set-buffer-file-coding-system)
          ("F" . toggle-frame-fullscreen)
          ("e" . async-shell-command)
          ("E" . r-os-with-shell-open)
          ("t" . untabify)
          ("E" . r-start-everything)
          ("C" . move-to-column)
          (")" . check-parens)
          ("v" . r-start-vpn)
          ("V" . r-start-vpn2)
          ("M" . r-q-minor-mode)
          ("(" . rdf-start-screen-record)
          ("S" . r-redef-environment-setup)
          ("s" . save-some-buffers)
          ("M-l" . toggle-frame-maximized)
          ("C-x C-c" . save-buffers-kill-terminal)
          :map redef-global-key-bindings-high-effort-map
          ("e" . gnus) ; read email
          :map redef-global-key-bindings-org-agenda-map
          ("a" . org-agenda-list)
          ("t" . org-todo-list)
          ("l" . org-insert-link) ; insert may be use many times, so use little l
          ("L" . org-store-link)
          ("q" . org-tags-view)
          ("p" . org-set-property)
          ("o" . r-org-open-at-point-emacs)
          ("c" . org-capture) ; to define temp tasks
          )
  :config
  (dotimes (count 52)
    (let* ((cur-char (cond
                      ((< count 26) (string (+ ?a count)))
                      ((< count 52) (string (+ ?A count -26)))
                      (t "?")))
           (eval-symbol (intern-soft (concat "ext-work-"
                                             cur-char
                                             "-internal"))))
      (when (and eval-symbol (fboundp eval-symbol))
        (define-key redef-global-key-bindings-interactive-map (kbd cur-char) eval-symbol)
        ))))
```


### redef theme setup <span class="tag"><span class="theme">theme</span></span> {#redef-theme-setup}

```emacs-lisp
(use-package redef-config
  :load-path "~/.emacs.d/redef/"
  :init
  ;; use 'fds-show-all' to check all fonts
  (set-face-attribute
   'default nil
   :font "-GOOG-Noto Sans Mono CJK SC-bold-normal-normal-*-*-*-*-*-*-0-iso10646-1")
  (setq rdf-theme-style
        (if (or (> (nth 2 (decode-time (current-time))) 18)
                (< (nth 2 (decode-time (current-time))) 8))
            'dark
          'light))
  (defun redef-theme-load (theme-style)
    (interactive)
    ;; command (customize-themes) list all known themes
    (let ((dark-theme-list '(light-blue dichromacy leuven adtaita
                                     tango tsdh-light whiteboard))
          (light-theme-list '(monokai tsdh-dark deeper-blue manoj-dark misterioso
                                      tango-dark wheatgrass womat)) ;; tango-dark has strange code in windows
          (theme-to-set (if (equal theme-style 'dark)
                            (if (member 'monokai (custom-available-themes))
                                'monokai
                              'tsdh-dark)
                          'light-blue)))
      ;; dark mean used at night, actualy is a light-theme
      (setq ext-dash-theme-used
            (if (memq theme-to-set dark-theme-list) nil t))
      (load-theme theme-to-set t)))
  (defun redef-theme-reload ()
    (interactive)
    (setq rdf-theme-style
          (if (or (> (nth 2 (decode-time (current-time))) 18)
                  (< (nth 2 (decode-time (current-time))) 8))
              'dark
            'light))
    (redef-theme-load rdf-theme-style))
  (setq title-dir (concat (file-name-directory
                           (getenv "EMACS_CONFIG"))
                          "./title"))
  (setq ext-rdf-title-list (with-temp-buffer
                             (dolist (file (directory-files title-dir))
                               (unless (member file '("." ".."))
                                 (insert-file-contents (concat title-dir "/" file))
                                 (insert "\n")))
                             (split-string (buffer-substring-no-properties
                                            (point-min) (point-max)) "[\n\r]+" t)))
  (setq ext-rdf-title-list-len (length ext-rdf-title-list))
  (setq ext-set-random-title
        (lambda () (set-frame-parameter nil 'title
                                        (nth (random ext-rdf-title-list-len)
                                             ext-rdf-title-list))))
  (run-with-idle-timer 52 t ext-set-random-title)
  (funcall ext-set-random-title)
  (redef-theme-load rdf-theme-style)
  :bind*
  (:map redef-global-key-bindings-high-effort-map
        ("R" . redef-theme-reload))
  )

```


### built in package <span class="tag"><span class="built_in">built-in</span></span> {#built-in-package}

```emacs-lisp
(use-package uniquify
  :defer 1
  :config
  (setq uniquify-buffer-name-style 'forward) ;unified buffer name
  )

(use-package recentf
  :defer 2
  :demand t
  :config
  (require 'recentf)
  (setq recentf-auto-cleanup 'never)
  (setq recentf-max-menu-items 25)
  (setq auto-save-list-file-prefix "~/../app_home/emacs/")
  (setq recentf-save-file "~/../app_home/emacs/recentf")
  (add-to-list 'recentf-keep 'file-remote-p)
  (recentf-mode 1)
  :bind*
  (:map redef-global-key-bindings-low-effort-map
        ("r" . recentf-open-files))
  )

(use-package elec-pair
  :defer 2
  :config
  (electric-pair-mode 1)
  )

(use-package ido
  :defer 2
  :config
  (unless (featurep 'helm-mode)
    (ido-mode t) ;enable ido-mode
    (setq ido-enable-flex-matching t)
    (ido-everywhere) ;C-x C-f C-f to find-file normal mode
    (setq ido-save-directory-list-file
          (funcall (lambda (new-file old-file) nil
                     (cond
                      ((file-readable-p new-file) new-file)
                      ((file-readable-p old-file) old-file)
                      (t new-file)))
                   "~/../app_home/ido/ido.last"
                   "~/../app_home/ido/.ido.last")))
  )

(use-package eww
  :defer 3
  :config
  (setq eww-download-directory "~/../app_home/eww/")
  )

(use-package bookmark
  :defer 4
  :bind (:map bookmark-map
              ("r" . bookmark-rename)
         :map bookmark-bmenu-mode-map
         ("M-o" . (lambda () (interactive)
                    (other-window 1))))
  :config
  (setq bookmark-default-file "~/.emacs.d/redef/bookmarks/bookmarks")
  (setq bookmark-save-flag 1) ;;save per one bookmark added
  )

(use-package url
  :defer 5
  :config
  (setq url-configuration-directory "~/../app_home/emacs/url/")
  )

(use-package ibuffer
  :defer 5
  :bind*
  (("C-x C-b" . ibuffer)
   (:map ibuffer-mode-map
         ("M-n" . nil) ; unbind for key conflict with global keybinding
         ("M-p" . nil) ; unbind for key conflict with global keybinding
         ("M-o" . nil) ; unbind for key conflict with global keybinding
         )))

(use-package ruby-mode
  :config
  (add-hook 'ruby-mode-hook (lambda () nil nil
                              (setq save-buffer-coding-system 'utf-8-unix))))

(use-package desktop
  :init
  (setq desktop-path '("~/../app_home/desktop/"))
  :config
  (setq
   desktop-load-locked-desktop nil ; don't load locked desktop file
   desktop-auto-save-timeout nil ; disable autosave desktop
   desktop-restore-frames t ; must restore window configure, used for eyebrowse mode
   desktop-restore-reuses-frames nil ; delete multi frames
   desktop-dirname (car desktop-path)
   )
  (add-hook 'desktop-after-read-hook
            (lambda () nil nil
              (funcall ext-set-random-title)
              (redef-theme-load rdf-theme-style)))
  (desktop-save-mode 1) ;; disable/enable desktop mode
  )

(use-package server
  :ensure nil
  :hook (after-init . server-mode))

(use-package helm-flyspell
  :if ext-helm-mode-used
  :ensure t
  :after (helm-mode)
  :demand t
  :bind*
  (:map redef-global-key-bindings-flycheck-map
        ("c" . helm-flyspell-correct))
  )

(use-package flyspell
  :demand t
  :bind*
  (:map redef-global-key-bindings-flycheck-map
        ("f" . flyspell-mode))
  :config
  (setq ispell-program-name "d:/yardf/program/hunspell/bin/hunspell.exe")
  (setq ispell-local-dictionary "en_GB")
  )

(use-package org
  :demand t
  :config
  (org-babel-do-load-languages
   'org-babel-load-languages
   '((C . t)
     (emacs-lisp . t)
     (ruby . t)
     (python . t)
     (dot . t)
     (plantuml . t)
     (haskell . t)
     (ein . t)
     (shell . t)
     ))
  (setq org-babel-python-command "python3")
  (setq org-use-sub-superscripts nil)
  (setq org-hide-emphasis-markers t)
  ;; default show content insead of showall
  ;; use TAB and S-TAB to expand-cycle local/global content
  (setq org-startup-folded 'content)

  :bind*
  (:map redef-global-key-bindings-org-agenda-map
        ("S" . org-schedule) ;; task start time
        ("D" . org-deadline) ;; task end time
        )
  )

(use-package eww
  :demand t
  :config
  (setq eww-search-prefix "https://google.com/search?q=")
  )

(use-package gud
  :demand t
  :config
  (when ext-mingw-gcc-program
    (setq gud-gdb-command-name
          (concat (file-name-directory ext-mingw-gcc-program)
                  "/gdb -i=mi"))
    )
  ;; disable company in gud, may lead emacs hang
  (add-hook 'gud-mode-hook (lambda () (company-mode -1)))
  )

(use-package sql
  :demand t
  :config
  (setq sql-connection-alist
        '((pgsql-root (sql-product 'postgres)
                      (sql-port 5432)
                      (sql-server "localhost")
                      (sql-user "postgres")
                      (sql-password (base64-decode-string "Mzc4cTEyMy0="))
                      (sql-database "postgres")) ;; root password postgres
          (pgsql-blog (sql-product 'postgres)
                      (sql-port 5432)
                      (sql-server "localhost")
                      (sql-user "blog") ; self blog database
                      (sql-password (base64-decode-string "Mzc4cTEyMy1ibG9n"))
                      (sql-database "blog"))
          ))
  :bind*
  (:map redef-global-key-bindings-low-effort-map
        ("q" . sql-connect)))

(use-package python
  :demand t
  :config
  (setq-default fill-column 79)
  (add-hook 'text-mode-hook 'turn-on-auto-fill)
  (add-hook 'python-mode-hook
            (lambda () (progn
                         (set-variable 'py-indent-offset 4)
                         (set-variable 'indent-tabs-mode nil))))
  )


```


### emacs options <span class="tag"><span class="options">options</span></span> {#emacs-options}

```emacs-lisp
(use-package redef-config
    :requires (redef-lib)
    :load-path "~/.emacs.d/redef/"
    :after (redef-lib)
    :init
    ;; Hiden startup screen
    (setq inhibit-startup-screen t)

    ;; Coding
    (setq default-buffer-file-coding-system 'utf-8) ;default create buffer

    ;; Tips
    (setq apropos-do-all t)   ;apropos wide find v, find f
    (fset 'yes-or-no-p 'y-or-n-p) ;for users prompt
    (show-paren-mode t) ;for paren auto show
    (column-number-mode nil) ;disable column show, this may slower edit
    (with-windows-nt
     (global-hl-line-mode 1) ;highlight current line
     )
    (setq visible-bell t)

    (setq make-backup-files nil) ;disable backup files(*~)
    (setq auto-save-default nil) ;disable auto-save, auto generated file(~*~)
    (setq-default abbrev-mode t)
    (setq default-tab-width 2)
    (setq tab-width 2)
    (setq-default indent-tabs-mode nil)
    ;; enable default disabled narrow command
    ;; use widden to unhidden narrowed part
    (put 'narrow-to-region 'disabled nil)

    ;; GUI
    (menu-bar-mode 0)
    (scroll-bar-mode 0)
    (tool-bar-mode 0)
    (global-linum-mode 0)
    (setq linum-format "%d:")
    (defun r-show-current-column-number () (interactive) (current-column))

    ;; initial buffer setting
    (setq initial-major-mode 'org-mode)
    (setq initial-scratch-message
          (concat
           "* scratch\n"
           "  "
           ))

    ;; debug when error happen
    (setq debug-on-error t)

    ;; simplize mode-lines
    (setq-default mode-line-format '("%e" mode-line-front-space
                                     ;; buffer info
                                     "%[" "%Z" " " mode-line-buffer-identification " "
                                     (-6 "%l") "-" (3 "%p") " "
                                     (:eval
                                      (propertize (format-mode-line mode-name)
                                                  'face 'font-lock-constant-face)
                                      )
                                     ;; project info
                                     (:eval
                                      (if (and (fboundp 'projectile-project-name)
                                               (projectile-project-p))
                                          (concat " | " (symbol-name (projectile-project-type)) ":" (projectile-project-name))
                                        ""))
                                     " "
                                     (vc-mode ("" vc-mode " | "))
                                     mode-line-misc-info mode-line-end-spaces))

    (setq source-directory (concat ext-emacs-source-dir "/src"))
    (setq find-function-C-source-directory source-directory)

    ;; start emacs server
    (add-hook 'after-init-hook 'server-start)
    ;;if file is system file, make it readonly
    (setq r-sys-file-safe-mode 1)
    (defun r-switch-sys-file-safe-mode ()
      (interactive)
      (if (> r-sys-file-safe-mode 0)
          (setq r-sys-file-safe-mode 0)
        (setq r-sys-file-safe-mode 1)))

    (defun rdf-make-sys-file-readonly ()
      (let ((filename-current (buffer-file-name))
            (readonly-flag nil)
            (readonly-filename-partern (list
                                        ".emacs.d/elpa/" ;; these files are installed packages
                                        "program/share/emacs/" ;; these files are system files
                                        )))
        (when filename-current
          (do ((partern_r readonly-filename-partern)) ((or (not partern_r) readonly-flag) nil)
              (setq readonly-flag (string-match (car partern_r) filename-current))
              (setq partern_r (cdr partern_r)))
          (when readonly-flag
            (read-only-mode r-sys-file-safe-mode)))))
    ;; monitor startup time
    (add-hook 'emacs-startup-hook
              (lambda ()
                (message "Emacs ready in %s with %d garbage collections."
                         (format "%.2f seconds"
                                 (float-time (time-subtract after-init-time
                                                            before-init-time)))
                         gcs-done)
                (add-hook 'find-file-hook 'rdf-make-sys-file-readonly)
                ))
    :bind*
    (:map redef-global-key-bindings-low-effort-map
          ("I" . r-switch-sys-file-safe-mode)
          ("O" . r-show-current-column-number)
          ("f" . ffap-alternate-file-other-window))
    )
```


## ext packages <span class="tag"><span class="ext">ext</span></span> {#ext-packages}


### use-package <span class="tag"><span class="use_package">use-package</span></span> {#use-package}

:init
: execute before package load

:config
: execute after a package is loaded

:ensure
: if a package is not installed, will install it auto

<!--listend-->

```emacs-lisp
(use-package package
  :config
  (add-to-list 'package-archives (cons "redef-melpa" rdf-emacs-local-mepa-dir)))
  ;;(setq use-package-always-pin 'redef-melpa) ;;alway setup from local dir
```


### elpa-mirror <span class="tag"><span class="elpa_mirror">elpa-mirror</span></span> {#elpa-mirror}

```emacs-lisp
(use-package elpa-mirror
  :ensure t
  :requires (package)
  :commands (rdf-package-install-all-ext-remote
             rdf-package-install-all-ext-local
             rdf-package-dump-all-installed)
  :bind* (("C-x p r" . rdf-package-install-all-ext-remote)
          ("C-x p l" . rdf-package-install-all-ext-local)
          ("C-x p s" . rdf-package-dump-all-installed))
  :init
  ;; "http://melpa.milkbox.net/packages/" is out of date
  (add-to-list 'package-archives '("melpa" . "https://melpa.org/packages/"))
  :config
  (setq elpamr-default-output-directory rdf-emacs-local-mepa-dir)
  (defun rdf-install-packages-from-melpa (package-list)
    (package-initialize)
    ;;("melpa" . "http://stable.melpa.org/packages/")
    (let ((package-archives '(("melpa" . "https://melpa.org/packages/")))
          (url-http-attempt-keepalives nil))
      (unless (buffer-live-p "*Packages*")
        (package-refresh-contents))
      (dolist (package package-list) (package-install package))))

  (defun rdf-dump-installed-packages-to-dir (local-dir)
    (let ((elpamr-default-output-directory local-dir))
      (elpamr-create-mirror-for-installed local-dir)))

  (defun rdf-install-packages-from-dir (package-list melpa-dir)
    (package-initialize)
    (let ((package-archives '(("redef-melpa" . melpa-dir))))
      (dolist (package package-list) (package-install package))))

  (defun rdf-package-install-all-ext-remote ()
    (interactive)
    (rdf-install-packages-from-melpa rdf-ext-melpa-package-list))
  (defun rdf-package-install-all-ext-local ()
    (interactive)
    (rdf-install-packages-from-dir rdf-ext-melpa-package-list
                                   rdf-emacs-local-mepa-dir))
  (defun rdf-package-dump-all-installed ()
    (interactive)
    (rdf-dump-installed-packages-to-dir rdf-emacs-local-mepa-dir))
)
```


### guide-key <span class="tag"><span class="guide_key">guide-key</span></span> {#guide-key}

```emacs-lisp
(use-package dash
  :ensure t)
(use-package popwin
  :ensure t)
(use-package s
  :ensure t)
(use-package guide-key
  :ensure t
  :requires (popwin dash s)
  :config
  (setq guide-key/guide-key-sequence
        '(
          "M-i" ; for interactive command
          "M-h" ; for high cost command
          "M-l" ; for low cost command

          "M-l m" ; for multi-cursor
          "M-s" ;for yasnippet
          "M-j" ;for projectile
          "C-c e" ;for emms
          "M-e" ;for eyebrowse(default C-c C-w)

          "M-b"   ;for bookmark+(M-b difficult to touch)
          "C-t"   ;for gtags/dumb-jump
          "M-c"   ;for cpp development

          "M-r" ;for inf-ruby
          "M-r M-g" ;for rails goto
          "M-k" ;for haskell-mode
          "M-d" ;for desktop commands
          "M-w" ;for web commands
          "M-a" ;for org and agenda commands
          "M-f" ;for flycheck and langtool commands
          "M-q" ;for org-roam-daily
          "M-m" ;for email commands
          "C-x p" ; package commands
          "M-x" ;for python commands
          "M-t" ;for rust commands
          "M-g" ;for sagemath commands

          "C-c" ;common prefix
          ;; "C-x" ;common prefix mut not defined here
          ))
  (setq guide-key/idle-delay 1.0)
  (guide-key-mode 1)
  (setq guide-key/popup-window-position 'bottom))
```


### keyfreq <span class="tag"><span class="keyfreq">keyfreq</span></span> {#keyfreq}

```emacs-lisp
(use-package keyfreq
  :ensure t
  :config
  (keyfreq-mode 1)
  (keyfreq-autosave-mode 1)
  (setq keyfreq-excluded-commands
        '(self-insert-command
          org-self-insert-command
          image-next-file
          image-next-line
          undo-tree-undo
          forward-char
          backward-char
          previous-line
          next-line))
  :bind
  (:map redef-global-key-bindings-low-effort-map
        ("k" . keyfreq-show))
  )
```


### undo-tree <span class="tag"><span class="undo_tree">undo-tree</span></span> {#undo-tree}

```emacs-lisp
(use-package undo-tree
  :ensure t
  :demand t
  :bind*
  (("C-u" . undo-tree-undo)
   ("C-r" . undo-tree-redo))
  :config
  (global-undo-tree-mode))
```


### company <span class="tag"><span class="company">company</span></span> {#company}

use 'company-backends' to view current mode's backends
use 'company-diag' to view current using backend

```emacs-lisp
(use-package color
  :ensure t)
(use-package company
  :ensure t
  :demand t
  :requires (color)
  :bind (:map company-active-map
         ("C-n" . company-select-next)
         ("C-p" . company-select-previous))
  :custom-face
  (company-scrollbar-bg ((t (:inherit :background "#000000"))))
  (company-tooltip ((t (:inherit default :background "#ffffff" :foreground "#000000"))))
  (company-tooltip-common ((t (:inherit font-lock-constant-face))))
  (company-tooltip-selection ((t (:inherit font-lock-function-name-face))))
  (company-scrollbar-fg ((t (:inherit :background "#000000"))))
  :config
  (add-hook 'after-init-hook 'global-company-mode)
  (setq company-idle-delay 0.5)
  (setq company-clang-executable ext-company-clang-executable)
  ;; custom backends according to major mode
  (setq company-backends
        '((company-files ; path
           company-keywords
           company-capf ; completion-at-point-functions
           company-yasnippet)
          (company-abbrev
           company-dabbrev)))
  (defun r-company-gen-local-backends (backend-list)
    (let ((cur-global-backends company-backends)
          (new-backends-list (make-local-variable 'company-backends)))
      (dolist (item cur-global-backends)
        (add-to-list new-backends-list item))
      (add-to-list new-backends-list backend-list)))
  (add-hook 'emacs-lisp-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-elisp))))
  (add-hook 'inferior-emacs-lisp-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-elisp))))
  (add-hook 'org-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-elisp))))
  (add-hook 'c-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-clang
                 company-gtags
                 company-etags))))
  (add-hook 'html-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-css))))
  (add-hook 'css-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-css))))
  (add-hook 'js-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-css))))
  )
(use-package company-tabnine
  :if nil ; seems not so useful and slow
  :ensure t
  :demand t
  :after (company)
  :config
  (add-to-list 'company-backends #'company-tabnine)
  (setq company-idle-delay 0)
  (setq company-show-numbers 0))
```


### org-super-agenda <span class="tag"><span class="org">org</span><span class="org_super_agenda">org-super-agenda</span></span> {#org-super-agenda}

```emacs-lisp
;;; store link must select the uniq line, and change the link after the context of that line changed
;;(add-hook 'org-create-file-search-functions ext-org-search-string-func)
;;(add-hook 'org-execute-file-search-functions ext-org-search-string-func)

;;;
;;; C-c C-t  change state
;;; C-c C-q  insert tag
;;; C-c ,    insert priority
;;; C-c a    list agendas
;;; C-c c    start capture
;;; C-c C-s  schedule date
;;; C-c C-d  deadline date
;;;

(use-package org
  :config
  (setq org-todo-keywords
        ;; avoid use too many items, will difficult to clarify from.
        ;; habits must use TODO keywords, so don't use LOOP like keys
        ;;
        ;; TODO: plan to do task, or doing habit task, must go first
        ;; PLANING: some big task, need think what and How
        ;; DOING: already doing task, not contain repeat task
        ;; POSTPONE: partly done and delayed for some reason
        ;; DONE: target achived
        ;; CANCEL: failed to achive target
        ;;
        '((sequence "TODO(t)" "PLANING(h)" "DOING(i)" "POSTPONE(p)" "|" "CANCEL(c)" "DONE(d)")))
  (setq  org-link-file-path-type 'relative)
  (setq org-log-done 'time)
  (setq org-agenda-span 'month)
  (setq org-directory "~/.emacs.d/redef/org")
  (setq org-agenda-files (concat org-directory "/agendas"))
  (setq org-default-notes-file (concat org-directory "/captures.org"))
  (setq org-capture-templates
        '(("t" "Task to be done" entry (file+headline org-default-notes-file "TASK")
           "* TODO %U %?\n")
          ("i" "Idea to try" entry (file+headline org-default-notes-file "IDEA")
           "* About %? \n %U")
          ("p" "Plan to be done" entry (file+headline org-default-notes-file "PLAN")
           "* For %? \n %U")))
  (setq org-hide-leading-stars t)
  (org-indent-mode t)
  ;;confit html export
  (with-eval-after-load 'ox
    (require 'ox-hugo)
    (add-to-list 'org-hugo-external-file-extensions-allowed-for-copying
                 "md")
    (defun rdf-export-roam-to-hugo ()
      (interactive)
      (mapc (lambda (file)
              (with-current-buffer
                  (find-file-noselect file)
                (org-hugo-export-wim-to-md)))
            (directory-files-recursively org-roam-directory ".*.org"))
      (start-process "*hugo-gen*" nil "python3" (concat org-hugo-base-dir "/content/d3/dump_roam_db.py")))
    (setq org-hugo-base-dir (concat ext-root-workspace "/hugo")))
  (require 'ox-publish)
  (defun rdf-export-blog-to-jekyll-filter (output backend info)
    (when (eq backend 'html)
      (concat "---\n"
              ;; For org-mode share assets directory
              "permalink: /:year/:title:output_ext\n"
              ;; For minimal-mistakes-jekyll theme
              "toc_label: Contents\n"
              "toc: true\n"
              "toc_sticky: true\n"
              "layout: single\n"
              "---\n"
              output)))
  (defun org-html-publish-to-jekyll-html (PLIST FILENAME PUB-DIR)
    (let ((org-export-filter-final-output-functions '(rdf-export-blog-to-jekyll-filter))
          (org-publish-use-timestamps-flag nil))
      (org-html-publish-to-html PLIST FILENAME PUB-DIR))
    )

  ;;; fix org export to html img-link error
  ;;; https://emacs.stackexchange.com/questions/27060/embed-image-as-base64-on-html-export-from-orgmode
  ;; (defun replace-in-string (what with in)
  ;; (replace-regexp-in-string (regexp-quote what) with in nil 'literal))

  ;; (defun org-html--format-image (source attributes info)
  ;;   (progn
  ;;     (setq source (replace-in-string "%20" " " source))
  ;;     (format "<img src=\"data:image/%s;base64,%s\"%s />"
  ;;             (or (file-name-extension source) "")
  ;;             (base64-encode-string
  ;;              (with-temp-buffer
  ;;                (insert-file-contents-literally source)
  ;;                (buffer-string)))
  ;;             (file-name-nondirectory source))))

  (setq org-image-actual-width nil)

  (setq org-publish-project-alist
        (list
         ;; for notes
          (list "org-html-theme"
                :base-directory (concat rdf-fdir "/bext/code/localize/examples/org-html-themes/")
                :base-extension "css\\|js"
                :publishing-directory (concat rdf-fdir "/rdoc/html/org-html-themes")
                :recursive t
                :publishing-function 'org-publish-attachment
                )
          (list "org-notes-theme"
                :base-directory (concat rdf-fdir "/rdoc/html/org-html-themes")
                :base-extension "css\\|js"
                :publishing-directory (concat rdf-fdir "/rdoc/html/notes/")
                :recursive t
                :publishing-function 'org-publish-attachment
                )
          (list "org-notes"
                :base-directory (concat rdf-fdir "/redef/repos/rdf-mix/roam/")
                :base-extension "org"
                :publishing-directory (concat rdf-fdir "/rdoc/html/notes/")
                :recursive t
                :publishing-function 'org-html-publish-to-html
                :headline-levels 4
                :auto-preamble t
                )
          (list "org-notes-static"
                :base-directory (concat rdf-fdir "/redef/repos/rdf-mix/roam/")
                :base-extension "css\\|js\\|png\\|jpg\\|gif\\|pdf\\|mp3\\|ogg\\|swf"
                :publishing-directory (concat rdf-fdir "/rdoc/html/notes/")
                :recursive t
                :publishing-function 'org-publish-attachment
                )
          (list "notes"
                ;; will run sequence
                :components '("org-html-theme" "org-notes-theme" "org-notes" "org-notes-static"))
        ;; for blogs
          (list "org-blogs"
                :base-directory (concat rdf-fdir "/workspace/blog/__all")
                :base-extension "org"
                :publishing-directory (concat rdf-fdir "/workspace/blog/_posts/")
                :recursive t
                :publishing-function 'org-html-publish-to-jekyll-html
                )
        ))
  :bind*
  ;;pop-up mark ring, use org-open-at-point to open a link
  ("C-c p" . org-mark-ring-goto)
  )
(use-package ht
  :ensure t)
(use-package ts
  :ensure t)
(use-package org-super-agenda
  :ensure t
  :requires (ht ts org)
  :config
  (setq org-super-agenda-groups
        '(
          (:name "Today" ;; repeat need task
                 :todo "TODAY"
                 :order 1)
          (:name "Repeat Task" ;; repeat need task
                 :todo "LOOP"
                 :habit t
                 :order 5)
          (:order-multi ;; For life
           (8 (:name "Family"
                     :tag "family")
              (:name "Friends"
                     :tag "friend")
              (:name "Redef"
                     :tag "redef")))
          (:name "Draft or temparay task to be collected"
                 :tag ("draft" "temp" "tmp")
                 :order 9)
          (:order-multi ;; For 技术
           (6 (:name "Programming Language"
                     :tag ("ruby" "c" "c++" "elisp" "python"))
              (:name "Web"
                     :tag ("web"))
              (:name "Emacs"
                     :tag "emacs")
              (:name "Firefox"
                     :tag "firefox")))
          (:priority<= "B" ;;high priority
                       :order 2)))
  (org-super-agenda-mode 1))
```


### yaml-mode <span class="tag"><span class="yaml">yaml</span></span> {#yaml-mode}

```emacs-lisp
(use-package yaml-mode
  :ensure t
  :mode ("\\.clang-format\\'" . yaml-mode)
  :bind (:map yaml-mode-map
              ("C-m" . newline-and-indent)))
```


### inf-ruby <span class="tag"><span class="inf">inf</span><span class="ruby">ruby</span><span class="ruby">ruby</span></span> {#inf-ruby}

```emacs-lisp
(use-package inf-ruby
  :ensure t
  :demand t
  :hook (ruby-mode . inf-ruby-minor-mode)
  :init
  (setq inf-ruby-default-implementation "pry")
  :config
  (autoload 'inf-ruby-minor-mode "inf-ruby" "Run an inferior Ruby process" t)
  (with-windows-nt
   (add-to-list 'inf-ruby-implementations' ("pry". "Pry")))
  (defun r-run-ruby-code (&rest ruby-code)
    (unless (get-buffer-process
             (or (inf-ruby-buffer) inf-ruby-buffer))
      (inf-ruby)) ; start inf-ruby if not start yet
    (with-temp-buffer
      (insert (string-join ruby-code "\n"))
      (ruby-send-buffer)))
  :bind
  (:map redef-global-key-bindings-ruby-map
        ("e" . inf-ruby) ;;enter irb session
        ("f" . ruby-load-file) ;;execute ruby file
        ("s" . ruby-switch-to-inf) ;;switch to irb session
        ("r" . ruby-send-region)
        ("R" . ruby-send-region-and-go))
  )
```


### rubocop <span class="tag"><span class="rubocop">rubocop</span><span class="ruby">ruby</span></span> {#rubocop}

if report error, run inf-ruby firstly.

```emacs-lisp
(use-package rubocop
  :ensure t
  :hook (ruby-mode . rubocop-mode)
  :bind
  (:map redef-global-key-bindings-ruby-map
        ("c" . rubocop-check-current-file)
        ("C" . rubocop-check-directory))
  )
```


### robe <span class="tag"><span class="robe">robe</span><span class="ruby">ruby</span></span> {#robe}

```emacs-lisp
;; not used in windows
```


### enh-ruby-mode <span class="tag"><span class="enh_ruby">enh-ruby</span><span class="ruby">ruby</span></span> {#enh-ruby-mode}

```emacs-lisp
;;; enh-ruby-mode
;;(setq use-enh-ruby-mode nil)
;;
;; if disable enh-ruby-mode, will has no autocomplete feature
;; but default ruby-mode is fast enough, enh-ruby-mode is slow and
;; do end align has some issue. This can be done by pry function.
;;
;; Suggest to disable enh-ruby-mode
;;
;;(when use-enh-ruby-mode
;;  (add-to-list 'load-path (expand-file-name "~/.emacs.d/ext/ruby/enhanced-ruby-mode-master/"))
;;  (autoload 'enh-ruby-mode "enh-ruby-mode" "Major mode for ruby files" t)
;;  (add-to-list 'auto-mode-alist '("\\.rb$\\|\\.pryrc$\\|Rakefile" . enh-ruby-mode))
;;  (add-to-list 'interpreter-mode-alist '("ruby" . enh-ruby-mode))
  ;; optional
;;  (when (boundp 'ext-ruby-program)
;;    (setq enh-ruby-program ext-ruby-program))
;;  (remove-hook 'enh-ruby-mode-hook 'erm-define-faces) ;;don't overwrite the define-faces, using (get-text-property (point) 'font-lock-face) to debug
;;  (add-hook 'enh-ruby-mode-hook 'inf-ruby-minor-mode)
;;  (add-hook 'enh-ruby-mode-hook 'rubocop-mode))
```


### magit <span class="tag"><span class="magit">magit</span></span> {#magit}

```emacs-lisp
(use-package async
  :ensure t)
(use-package dash
  :ensure t)
(use-package with-editor
  :ensure t)
(use-package transient
  :ensure t)
(use-package magit
  :ensure t
  :requires (async dash with-editor transient)
  :custom
  (magit-auto-revert-mode nil)
  :bind
  (:map redef-global-key-bindings-high-effort-map
        ("m" . magit-status)
        ("i" . magit-init)
        ("c" . magit-clone))
  :init
  (with-windows-nt
   (setq magit-git-executable ext-git-executable-program)
   (add-to-list 'auto-coding-alist '("COMMIT_EDITMSG" . utf-8)))
  :config
  (magit-auto-revert-mode -1)
  ;;
  ;; if do not load magit
  ;; when edit remote files, an error will happen
  ;;
  (require 'magit)
  )
```


### projectile <span class="tag"><span class="projectile">projectile</span></span> {#projectile}

```emacs-lisp
(use-package projectile
  :ensure t
  :demand t
  :init
  (setq projectile-cache-file "~/../app_home/projectile/projectile.cache")
  (setq projectile-known-projects-file "~/../app_home/projectile/projectile-bookmarks.eld")
  :config
  ;;(projectile-global-mode) ;;run this command if error "(wrong-type-argument hash-table-p nil)" happen
  (projectile-mode 1) ;;enable
  ;;Using Emacs Lisp for indexing files is really slow on Windows.
  ;;The alien indexing method uses external tools (e.g. git, find, etc) to speed up the indexing process.
  (setq projectile-indexing-method 'alien)
  (setq projectile-project-search-path
        (list (concat (getenv "R_WORKSPACE_DIR"))))
  (setq projectile-git-submodule-command nil) ; avoid echo error in windows
  :bind
  (:map redef-global-key-bindings-projectile-map
        ("s" . projectile-discover-projects-in-directory)
        ("i" . projectile-invalidate-cache)
        ("r" . projectile-remove-known-project)
        ("f" . projectile-find-file)
        )
  ;;
  ;; from existing project: (projectile-discover-projects-in-directory directory)
  ;;    known project type: git,Gemfile,Makefile,sconstruct,...
  ;;
  ;; create one:  .projectile
  ;;  IGNORE: -[dirname] -*.xxx
  ;;  ONLY CONTAIN: +[dirname]
  ;;
  )
```


### ggtags <span class="tag"><span class="ggtags">ggtags</span></span> {#ggtags}

```emacs-lisp
(if (featurep 'ggtags)
    (use-package ggtags
      :if (not ext-helm-mode-used)
      ))

```


### helm <span class="tag"><span class="helm">helm</span></span> {#helm}

```emacs-lisp
(use-package async
  :ensure t)
(use-package popup
  :ensure t)
;(require 'helm-config)
;(load "/home/thierry/elisp/helm-extensions/helm-extensions-autoloads.el")
(use-package helm-mode
  :if ext-helm-mode-used
  :demand t
  :requires (async popup)
  :bind (
         :map helm-map
         ("<tab>" . helm-execute-persistent-action)
         ("C-i" . helm-execute-persistent-action)
         ("C-z" . helm-select-action))
  :bind* (
          ("C-x ;" . helm-M-x)
          ("C-x C-y" . helm-show-kill-ring)
          :map redef-global-key-bindings-low-effort-map
          ("i" . helm-imenu)
          ("g" . helm-recentf)
          ;; depend on 'everything' in windows
          ("L" . helm-locate) ; find in whole drive
          ("l" . r-locate-in-directory)
          )
  ;; disable UAC warning: install everything server OR disable NTFS index
  ;; disable NTFS index need db already create, or there has no result from es.exe

  :config
  (helm-mode 1)
  (setq helm-command-prefix "C-c h")
  (defun r-locate-in-directory ()
    (interactive)
    (let ((helm-locate-command
           (concat "es -path "
                   default-directory
                   " %s %s")))
      (call-interactively 'helm-locate)))
  (setq helm-split-window-in-side-p           t ; open helm buffer inside current window, not occupy whole other window
        helm-move-to-line-cycle-in-source     t ; move to end or beginning of source when reaching top or bottom of source.
        helm-ff-search-library-in-sexp        t ; search for library in `require' and `declare-function' sexp.
        helm-scroll-amount                    8 ; scroll 8 lines other window using M-<next>/M-<prior>
        helm-ff-fuzzy-matching                t
        helm-projectile-fuzzy-match           t
        helm-lisp-fuzzy-completion            t
        helm-ff-file-name-history-use-recentf nil)
  (setq helm-M-x-fuzzy-match t) ;; optional fuzzy matching for helm-M-x
  (setq woman-manpath (list
                       (concat (getenv "emacs_dir") "/share/man/")
                       )) ;no match man-reader, so this command has no usage in windows
  (add-to-list 'helm-sources-using-default-as-input 'helm-source-man-pages) ;open man at point
  (helm-autoresize-mode t)
  ;; this is patch function of helm-display-buffer-in-own-frame
  (defun rdf-helm-display-buffer-in-own-frame (buffer &optional resume)
  "Display helm buffer BUFFER in a separate frame.

Function suitable for `helm-display-function',
`helm-completion-in-region-display-function'
and/or `helm-show-completion-default-display-function'.

See `helm-display-buffer-height' and `helm-display-buffer-width' to
configure frame size.

Note that this feature is available only with emacs-25+."
  (cl-assert (and (fboundp 'window-absolute-pixel-edges)
                  (fboundp 'frame-geometry))
             nil "Helm buffer in own frame is only available starting at emacs-25+")
  (if (not (display-graphic-p))
      ;; Fallback to default when frames are not usable.
      (helm-default-display-buffer buffer)
    (setq helm--buffer-in-new-frame-p t)
    (let* ((pos (window-absolute-pixel-position))
           (half-screen-size (/ (display-pixel-height x-display-name) 2))
           (frame-info (frame-geometry))
           (prmt-size (length helm--prompt))
           (line-height (frame-char-height))
           tab-bar-mode
           (default-frame-alist
             (if resume
                 (buffer-local-value 'helm--last-frame-parameters
                                     (get-buffer buffer))
               `((width . ,helm-display-buffer-width)
                 (height . ,helm-display-buffer-height)
                 (tool-bar-lines . 0)
                 (left . ,(/ (- (display-pixel-width x-display-name) (* helm-display-buffer-width (frame-char-width))) 2))
                 (top . ,(/ (- (display-pixel-height x-display-name) (* helm-display-buffer-height (frame-char-height))) 2))
                 (title . "Helm")
                 (undecorated . ,helm-use-undecorated-frame-option)
                 (background-color . ,(or helm-frame-background-color
                                          (face-attribute 'default :background)))
                 (foreground-color . ,(or helm-frame-foreground-color
                                          (face-attribute 'default :foreground)))
                 (alpha . ,(or helm-frame-alpha 100))
                 (vertical-scroll-bars . nil)
                 (menu-bar-lines . 0)
                 (fullscreen . nil)
                 (visibility . ,(null helm-display-buffer-reuse-frame))
                 (minibuffer . t))))
           display-buffer-alist)
      ;; Display minibuffer above or below only in initial session,
      ;; not on a session triggered by action, this way if user have
      ;; toggled minibuffer and header-line manually she keeps this
      ;; setting in next action.
      (unless (or helm--executing-helm-action resume)
        ;; Add the hook inconditionally, if
        ;; helm-echo-input-in-header-line is nil helm-hide-minibuffer-maybe
        ;; will have anyway no effect so no need to remove the hook.
        (add-hook 'helm-minibuffer-set-up-hook 'helm-hide-minibuffer-maybe)
        (with-helm-buffer
          (setq-local helm-echo-input-in-header-line nil
                      ;; don't set input in header line
                      ;;(not (> (cdr pos) half-screen-size))
                      )))

      (helm-display-buffer-popup-frame buffer default-frame-alist)
      ;; When frame size have been modified manually by user restore
      ;; it to default value unless resuming or not using
      ;; `helm-display-buffer-reuse-frame'.
      ;; This have to be done AFTER raising the frame otherwise
      ;; minibuffer visibility is lost until next session.
      (unless (or resume (not helm-display-buffer-reuse-frame))
        (set-frame-size helm-popup-frame
                        helm-display-buffer-width
                        helm-display-buffer-height)))
    (helm-log-run-hook 'helm-window-configuration-hook)))
  (setq helm-display-function 'rdf-helm-display-buffer-in-own-frame
        helm-display-buffer-reuse-frame t
        helm-display-buffer-width (/ (frame-width) 2)
        helm-display-buffer-height (/ (frame-height) 2)
        helm-autoresize-max-height 50
        helm-autoresize-min-height 5
        helm-use-undecorated-frame-option t)
  (add-hook 'after-init-hook (lambda () (helm-mode 1)))
  )

(use-package helm-ag
  :if ext-helm-mode-used
  :after (helm-mode))

(use-package swiper-helm
  :if ext-helm-mode-used
  :after (helm-mode))

(use-package helm-projectile
  :if ext-helm-mode-used
  :ensure t
  :after (helm-mode projectile)
  :demand t
  :bind* ; use helm-projectile-find-file override projectile-find-file
  (:map redef-global-key-bindings-projectile-map
        ("o" . helm-projectile-switch-project)
        ("f" . helm-projectile-find-file))
  )

(use-package helm-gtags
  :if ext-helm-mode-used
  :after (helm-mode)
  :ensure t
  :demand t
  :config
  (add-hook 'c-mode-hook (lambda () (helm-gtags-mode 1)))
  :bind*
  (:map redef-global-key-bindings-gtags-map
        ("C-t" . helm-gtags-create-tags)
        ("C-u" . helm-gtags-update-tags)
        ("h" . helm-gtags-dwim)
        ("C-h" . r-find-definition)
        ("r" . helm-gtags-find-rtag)
        ("C-r" . r-find-reference)
        ("p" . helm-gtags-pop-stack)
        ("C-p" . r-find-pop-stack)
        ("s" . helm-gtags-find-pattern)
        ("C-s" . r-find-symbol)
        ("C-f" . r-navi-stack-forward)
        ("C-b" . r-navi-stack-backward)
        ))
```


### ivy <span class="tag"><span class="ivy">ivy</span></span> {#ivy}

like helm

```emacs-lisp
(use-package swiper
  :ensure t
  :bind
  ("C-s" . swiper))
(use-package counsel
  :if (not ext-helm-mode-used)
  :ensure t
  :bind*
  (:map redef-global-key-bindings-low-effort-map
        ("i" . counsel-imenu))
  )
(use-package counsel-projectile
  :if (not ext-helm-mode-used)
  :after (counsel projectile)
  :ensure t
  :bind
  (:map redef-global-key-bindings-projectile-map
        ("o" . counsel-projectile-switch-project)
        ("f" . counsel-projectile-find-file)))
(use-package ivy
  :if (not ext-helm-mode-used)
  :after (ivy-todo counsel swiper)
  :config
  (ivy-mode 1)
  (setq ivy-use-virtual-buffers t)
  (setq enable-recursive-minibuffers t)
  )
```


### ace-window <span class="tag"><span class="ace">ace</span><span class="window">window</span></span> {#ace-window}

fast jump between windows

```emacs-lisp
(use-package avy
  :ensure t)
(use-package ace-window
  :requires (avy)
  :ensure t)
```


### visual-regexp <span class="tag"><span class="visual">visual</span><span class="regexp">regexp</span></span> {#visual-regexp}

visualable while query regexp replace

```emacs-lisp
(use-package visual-regexp
  :ensure t
  :bind ("C-x q" . vr/query-replace))
```


### eyebrowse <span class="tag"><span class="eyebrowse">eyebrowse</span></span> {#eyebrowse}

workspace manage
use `list-faces-display` to show all faces.
use `list-colors-display` to show all color names.

```emacs-lisp
(use-package eyebrowse
  :ensure t
  :config
  (add-to-list 'window-persistent-parameters '(window-side . writable)) ;; add this if need to store side window
  (add-to-list 'window-persistent-parameters '(window-slot . writable))
  (eyebrowse-mode t)
  (setq eyebrowse-mode-line-style t)
  (set-face-attribute 'eyebrowse-mode-line-active nil :foreground "LightSeaGreen")
  (defun r-eyebrowse-dump-to-tmp-from (slot)
    ;; dump workspace config to tmp(8) workspace
    (interactive (list (if (numberp current-prefix-arg)
                           current-prefix-arg
                         (eyebrowse--read-slot))))
    (when slot
      (eyebrowse-switch-to-window-config slot)
      (let* ((window-configs (eyebrowse-get 'window-configs)))
        (eyebrowse-switch-to-window-config 8)
        (eyebrowse--set 'window-configs window-configs)
        )))
  :bind* (
          ("M-1" . eyebrowse-switch-to-window-config-1)
          ("M-2" . eyebrowse-switch-to-window-config-2)
          ("M-3" . eyebrowse-switch-to-window-config-3)
          ("M-4" . eyebrowse-switch-to-window-config-4)
          ("M-5" . eyebrowse-switch-to-window-config-5)
          ("M-6" . eyebrowse-switch-to-window-config-6)
          ("M-7" . eyebrowse-switch-to-window-config-7)
          ("M-8" . eyebrowse-switch-to-window-config-8)
          ("M-9" . eyebrowse-switch-to-window-config-9)
          ("M-0" . eyebrowse-switch-to-window-config-0)
          :map redef-global-key-bindings-eyebrowse-map
          ("a" . eyebrowse-create-window-config)
          ("e" . eyebrowse-switch-to-window-config-1)
          ("c" . eyebrowse-close-window-config)
          ("s" . eyebrowse-switch-to-window-config)
          ("r" . eyebrowse-rename-window-config)
          ("l" . eyebrowse-last-window-config)
          ("M-p" . eyebrowse-prev-window-config)
          ("M-n" . eyebrowse-next-window-config)
          ("d" . r-eyebrowse-dump-to-tmp-from)
          ))

(use-package eyebrowse-restore
  :demand t
  :after (eyebrowse)
  :load-path "~/.emacs.d/ext/eyebrowse-restore/"
  :config
  (eyebrowse-restore-mode))
```


### multiple-cursors <span class="tag"><span class="multiple">multiple</span><span class="cursors">cursors</span></span> {#multiple-cursors}

```emacs-lisp
(use-package multiple-cursors
  :ensure t
  :demand t
  :bind
  (:map redef-global-key-bindings-low-effort-map
        ("me" . mc/edit-lines)
        ("mn" . mc/mark-next-like-this)
        ("mp" . mc/mark-previous-like-this)
        ("ma" . mc/mark-all-like-this)))
```


### yasnippet <span class="tag"><span class="yasnippet">yasnippet</span></span> {#yasnippet}

```emacs-lisp
(use-package yasnippet-classic-snippets)
(use-package yasnippet
  :requires (cl-lib)
  :ensure t
  :demand t
  :after (yasnippet-classic-snippets)
  :config
  (setq yas-snippet-dirs
        '("~/.emacs.d/ext/yasnippet/yasnippets-template/" ; contain user defined snippets
          ;; yas-installed-snippets-dir ; contain default snippets, currently not used
          yasnippet-classic-snippets-dir
          ))
  (add-hook 'yas-minor-mode-hook
            (lambda ()
              (yas-activate-extra-mode 'fundamental-mode)))
  (yas-global-mode 1) ;; or M-x yas-reload-all if you've started YASnippet already.
  :bind
  (:map redef-global-key-bindings-snippet-map
        ("n" . yas-new-snippet)
        ("v" . yas-visit-snippet-file)
        ("t" . yas-tryout-snippet)
        ("l" . yas-load-snippet-buffer)
        ("c" . yas-load-snippet-buffer-and-close)))
;; using command 'yas-describe-tables' to study yas in different mode

;;; document refer yasnippet/doc/snippet-development.org #Template Syntax
;;
;; $0 last point
;; $N tab pos
;; $<
;; `elisp` run lisp code while expand
;; ${N:default}
;; ${N:$(lisp code)}
;;
;; # --   split comment with snippet, upper is comment, below is snippet
;;
```


### graphviz-dot <span class="tag"><span class="graphviz">graphviz</span><span class="dot">dot</span></span> {#graphviz-dot}

graphviz tool

```emacs-lisp
(use-package graphviz-dot-mode
  :ensure t
  :init
  (setq default-tab-width 4)
  :config
  (setq graphviz-dot-dot-program ext-dot-program)
  (add-hook 'org-src-mode-hook
            (lambda () (add-to-list 'org-src-lang-modes
                                    '("dot" . graphviz-dot))))
  (setq org-confirm-babel-evaluate (lambda (lan body)
                                     (cond
                                      ((equal lan "dot") nil)
                                      (t t)))) ;; C-c C-c no need to confirm, only dot
  )

```


### emms <span class="tag"><span class="emms">emms</span></span> {#emms}

music and movie player

help
: press "?"

playlist
: 1.  in emms buffer press "b" to set current playlist
    2.  press "a" in any playlist to add track to current
    3.  press "D" or "C-k" to remove track from playlist
    4.  press "C-x C-s" save current playlist to a playlist file

need modify emms code to fix lyrics display issue:
`emms-track` will return a invalid type if not disable emms cache, don't
know why. eg. `(emms-track 'file "xxx.mp3")`, correct type should be `"file"`,
but always return `"plalist"`.

```emacs-lisp
(use-package cl-lib
  :ensure t)

(use-package emms
  :requires (cl-lib)
  :ensure t
  :init
  (setq emms-directory "~/../app_home/emms/")
  :config
  (require 'emms-setup)
  (emms-all)
  (emms-default-players)
  (define-emms-simple-player mplayer '(file url)
    (regexp-opt '(".ape" ".flac" ".wav" ".mp3" ".wma"
                  ".ogg" ".mpg" ".mpeg" ".wmv" ".mov"
                  ".avi" ".divx" ".ogm" ".asf" ".mkv" "http://" "mms://"
                  ".rm" ".rmvb" ".mp4" ".vob" ".m4a" ".flv" ".ogv" ".pls"))
    "mplayer" "-slave" "-quiet" "-really-quiet" "-fullscreen")
  (setq emms-playlist-buffer-name "*emms*")
  (emms-lyrics 1)
  (setq emms-source-file-default-directory (or ext-emms-music-dir "~/.emacs.d/emms/"))
  (setq emms-repeat-track nil) ;don't repeat one
  (setq emms-repeat-playlist nil) ;don't repeat by list
  (setq emms-random-playlist nil) ;don't do random play
  (emms-cache-disable)
  ;; (delete 'emms-player-mpv emms-player-list)
  (defun r-emms-audio-type-p (name)
    (if name
        (string-match-p (regexp-opt '(".mp3" ".wav" ".wma" ".ape")) name)
      nil))
  (defun r-emms-next ()
    (interactive)
    (with-current-buffer emms-playlist-buffer
      (if (r-emms-audio-type-p (emms-track-name
                                (emms-playlist-selected-track)))
          (emms-playlist-current-select-random) ;audio
        (emms-playlist-current-select-next)) ;video
      (emms-start)))
  (defun r-emms-play-playlist (file)
    (interactive (list (read-file-name "Playlist file: "
                                       emms-source-file-default-directory
                                       emms-source-file-default-directory
                                       t)))
    (let ((emms-playlist-buffer-name
           (concat "*emms-" (file-name-sans-extension (file-name-base file)) "*")))
      (with-current-buffer (or (get-buffer emms-playlist-buffer-name)
                               (emms-playlist-new emms-playlist-buffer-name))
        (emms-playlist-set-playlist-buffer)
        (emms-play-playlist file))))
  (defun r-emms-play-directory-tree (dir)
    (interactive
     (list (emms-read-directory-name "Play directory: "
                                     (emms-source-file-directory-hint)
                                     emms-source-file-default-directory
                                     t)))
    (with-current-buffer (or (get-buffer emms-playlist-buffer-name)
                             (emms-playlist-new emms-playlist-buffer-name))
      (emms-playlist-set-playlist-buffer)
      (emms-play-directory-tree dir)))
  (defun r-emms-playlist-save (format file)
    (interactive (list (emms-source-playlist-read-format)
                       (read-file-name "Store as: "
                                       emms-source-file-default-directory
                                       emms-source-file-default-directory
                                       nil)))
    (emms-playlist-save format file)
    ;; convert to utf-8
    (with-current-buffer (find-file file)
      (beginning-of-buffer)
      (end-of-line)
      (insert ";;; -*- coding: utf-8 -*-")
      (save-buffer)
      (kill-buffer)))
  (setq emms-player-next-function 'r-emms-next)
  ;; (setq emms-player-delay 10) ;; this will block emacs if >0
  (setq emms-track-description-function
        (lambda (track)
          (let ((type (emms-track-type track)))
            (cond ((eq 'file type)
                   (file-name-base (emms-track-name track)))
                  ((eq 'url type)
                   (emms-format-url-track-name (emms-track-name track)))
                  (t (concat (symbol-name type)
                             ": " (emms-track-name track)))))))
  (defun emms-lyrics-display-handler (lyric next-lyric line diff)
       "DIFF is the timestamp differences between current LYRIC and
          NEXT-LYRIC; LINE corresponds line number for LYRIC in `emms-lyrics-buffer'."
       (when (and next-lyric diff)
         (emms-lyrics-display (format emms-lyrics-display-format lyric) line)
         (when (and emms-lyrics-display-on-modeline emms-lyrics-scroll-p)
           (emms-lyrics-scroll lyric next-lyric diff))))
  :bind
  (:map redef-global-key-bindings-emms-map
   ("l" . r-emms-play-playlist)
   ("d" . r-emms-play-directory-tree)
   ("n" . emms-next)
   ("N" . emms-previous)
   ("p" . emms-pause)
   ("s" . emms-stop)
   ("C-s" . r-emms-playlist-save)
   ("r" . emms-random)
   ("m" . emms-metaplaylist-mode-go)))
```


### desktop+ <span class="tag"><span class="desktop">desktop</span></span> {#desktop-plus}

```emacs-lisp
(use-package desktop+
  :ensure t
  :after (desktop)
  :config
  (setq desktop+-base-dir (car desktop-path))
  (desktop+-add-handler 'ielm
    (lambda () (eql major-mode 'inferior-emacs-lisp-mode))
    (lambda () (list :ielm t))
    (lambda (name &rest args)
      (when (plist-get args :ielm)
        (ielm))))
  (desktop+-add-handler 'inf-ruby
    (lambda () (and (eql 'inf-ruby-mode
                         major-mode)
                    (member (buffer-name)
                            '("*pry*" "*ruby*"))))
    (lambda () (list :inf-ruby t))
    (lambda (name &rest args)
      (when (plist-get args :inf-ruby)
        (inf-ruby))))
  (desktop+-add-handler 'gnus
    (lambda () (and (eql major-mode
                         'gnus-group-mode)
                    (string-equal (buffer-name)
                                  "*Group*")))
    (lambda () (list :gnus t))
    (lambda (name &rest args)
      (when (plist-get args :gnus)
        (gnus))))
  (desktop+-add-handler 'message
    (lambda () (and (eql major-mode
                         'message-mode)
                    (string-equal (buffer-name)
                                  "*unsent mail*")))
    (lambda () (list :message t))
    (lambda (name &rest args)
      (when (plist-get args :message)
        (compose-mail))))
  (setq desktop+-special-buffer-handlers
        '(term-mode
          org-agenda-mode
          indirect-buffer
          shell-mode
          ielm
          inf-ruby
          gnus
          message))
  (defconst r-desktop+-rdf-default-desktop "rdf-head")
  (defun r-desktop-set-head (name)
    (interactive
     (list
      (completing-read "Desktop name: "
                       (remove "."
                               (remove ".."
                                       (directory-files desktop+-base-dir))))))
    (desktop+-load name)
    (desktop+-create r-desktop+-rdf-default-desktop)
    )
  (defun r-desktop-load-default ()
    (interactive)
    ;; this session will be automatic saved when session closed
    (desktop+-load r-desktop+-rdf-default-desktop))
  (defun r-desktop-create-default ()
    (interactive)
    ;; this session will be automatic saved when session closed
    (setq desktop-dirname (desktop+--dirname r-desktop+-rdf-default-desktop))
    (desktop-remove)
    (desktop+-create r-desktop+-rdf-default-desktop))
  :bind
  (:map redef-global-key-bindings-desktop-map
        ("c" . desktop+-create)
        ("l" . desktop+-load)
        ("d" . r-desktop-load-default)
        ("D" . r-desktop-create-default)
        ("r" . r-desktop-set-head)))
```


### wttrin <span class="tag"><span class="whether">whether</span></span> {#wttrin}

whether tool

```emacs-lisp
(use-package xterm-color
  :ensure t)
(use-package wttrin
  :ensure t
  :requires (xterm-color)
  :bind
  (:map redef-global-key-bindings-high-effort-map
        ("w" . r-wttrin))
  :config
  (setq wttrin-default-cities '("Suzhou" "Jingzhou" "Dongtai" "Beijing"))
  (defun r-wttrin ()
    (interactive)
    ;;solve wttr issue:
    ;; https://github.com/bcbcarl/emacs-wttrin/issues/16
    (let ((url-user-agent "curl"))
      (call-interactively 'wttrin)))
  )
```


### web <span class="tag"><span class="web">web</span></span> {#web}


#### js2-mode <span class="tag"><span class="js2">js2</span></span> {#js2-mode}

```emacs-lisp
(use-package js2-mode
  :ensure t
  :demand t
  :mode ("\\.js\\'" . js-mode)
  :config
  (add-hook 'js-mode-hook #'js2-minor-mode)
  :defer 8)
```


#### web-mode {#web-mode}

```emacs-lisp
(use-package web-mode
  :ensure t
  :mode ("\\.erb\\'" . web-mode))
```


#### simple-httpd <span class="tag"><span class="httpd">httpd</span></span> {#simple-httpd}

```emacs-lisp
(use-package simple-httpd
  :ensure t
  :config
  (setq httpd-root "d:/yardf/workspace/skewer/"))
```


#### impatient-mode <span class="tag"><span class="imp">imp</span></span> {#impatient-mode}

```emacs-lisp
(use-package htmlize
  :ensure t)
(use-package impatient-mode
  :requires (simple-httpd htmlize)
  :ensure t
  :demand t
  :config
  (defun r-web-debug-html ()
    (interactive)
    (httpd-start)
    (impatient-mode 1)
    (browse-url-default-browser "http://localhost:8080/imp/"))
  :bind* (:map redef-global-key-bindings-web-map
          ("h" . r-web-debug-html)))

;;;
;;; impatient-mode - debug html
;;; 1. httpd-start
;;; 2. impatient-mode
;;; 3. access localhost:8080/imp
;;;
```


#### skewer-mode <span class="tag"><span class="skewer">skewer</span></span> {#skewer-mode}

```emacs-lisp
(use-package skewer-mode
  :requires (simple-httpd skewer-html skewer-css skewer-repl)
  :ensure t
  :after (js2-mode)
  :hook ((js2-mode . skewer-mode)
         (css-mode . skewer-mode)
         (html-mode . skewer-mode))
  :bind
  (:map redef-global-key-bindings-low-effort-map
        ("k" . run-skewer)))
;;;
;;; skewer-mode  debug js
;;; 1. (setq httpd-root <root-dir>)
;;; 2. (httpd-start)
;;; 3. open "<root-dir>/demo.html"
;;; 4. in <root-dir>, run run-skewer
;;; 5. add <script src="http://localhost:8080/skewer"></script> in html
;;; 6. access http://localhost:8080/demo.html
;;; 7. start skewer-repl, debug js code in other files
;;;
```


#### markdown-mode <span class="tag"><span class="md">md</span><span class="markdown">markdown</span></span> {#markdown-mode}

```emacs-lisp
(use-package markdown-mode
  :ensure t
  :demand t
  :init
  (setq markdown-command (concat "perl " ext-markdown-program))
  )
```


#### indium <span class="tag"><span class="indium">indium</span><span class="nodejs">nodejs</span></span> {#indium}

```emacs-lisp
(use-package indium ;used to debug nodejs apps
  :ensure t
  :demand t
  :bind*
  (:map redef-global-key-bindings-web-map
        ("e" . r-web-debug-eletron-program)
        ("E" . r-web-start-eletron-program)
        )
  :config
  (setq indium-chrome-executable ext-chrome-program)
  (setq indium-chrome-data-dir "~/../app_home/indium/")
  (setq indium-client-debug t)
  (add-hook 'js-mode-hook #'indium-interaction-mode)
  (defun r-web-start-eletron-program ()
      (interactive)
      (start-process (file-name-base (substring default-directory 0 -1))
                     nil
                     "npm"
                     "start"))
  (defun r-web-debug-eletron-program ()
    (interactive)
    (let* ((app-name (file-name-base (substring default-directory 0 -1)))
           (app-config-file-name ".indium.json")
           (app-config-file (concat default-directory app-config-file-name))
           (app-args " ."))
      (if (fboundp 'r-run-ruby-code)
          (progn
            (let ((default-directory default-directory))
              (while (not (or (f-root-p default-directory)
                              (file-exists-p (concat default-directory app-config-file-name))))
                (setq default-directory (concat default-directory "/../")))
              (if (file-exists-p (concat default-directory app-config-file-name))
                  (setq app-config-file (concat default-directory app-config-file-name))))
            (unless (file-exists-p app-config-file)
              (r-run-ruby-code
               "require 'erb'"
               "require 'json'"
               (concat "output_file = %q("
                       app-config-file
                       ")")
               (concat "config_hash = {}")
               (concat "config_hash[:configurations] = [{}]")
               (concat "config_hash[:configurations][0][:name] = %q("
                       app-name
                       ")")
               (concat "config_hash[:configurations][0][:type] = 'node'")
               ;; if debug nodejs program, :program field shall be 'node'
               (concat "config_hash[:configurations][0][:program] = 'electron'")
               ;; insert 'debugger' in javascript code to set breakpoint to debug main process
               ;; if debug render process, use DevTools in main process, and debug is app UI
               (concat "config_hash[:configurations][0]['inspect-brk'] = 'true'")
               (concat "config_hash[:configurations][0][:args] = %q("
                       app-args
                       ")")
               "File.write(output_file, JSON.pretty_generate(config_hash))")
              (message "Electron debug file %s generated." app-config-file))
            (let ((default-directory (file-name-directory app-config-file)))
              (indium-launch)))
        (message "ERROR 'r-run-ruby-code' not defined, make sure inf-ruby installed."))))
  )
```


### email <span class="tag"><span class="email">email</span></span> {#email}


#### gnus <span class="tag"><span class="gnus">gnus</span></span> {#gnus}

```emacs-lisp
(use-package gnus
  :ensure t
  :init
  (defun rdf-emailrelay-send-email (emailrelay-runner emailrelay-cfg-dir)
    (start-process "emailrelay-client" nil emailrelay-runner
                   "--as-client" "smtp.gmail.com:587"
                   "--client-auth" (concat emailrelay-cfg-dir "/.emailrelay")
                   "--client-tls"
                   "--spool-dir" (concat emailrelay-cfg-dir "/pool/")))
  (defun rdf-emailrelay-server-start (emailrelay-runner emailrelay-cfg-dir)
    (start-process "emailrelay-server" nil emailrelay-runner
                   "--as-proxy" "smtp.gmail.com:25"
                   "--client-auth" (concat emailrelay-cfg-dir "/.emailrelay")
                   "--client-tls" "--log"
                   "--pid-file" (concat emailrelay-cfg-dir "/emailrelay.pid")
                   "--spool-dir" (concat emailrelay-cfg-dir "/pool/")))
  (defun rdf-send-email ()
    "Send email out to external server"
    (interactive)
    (unless (get-process "emailrelay-server")
      (rdf-emailrelay-server-start ext-emailrelay-program
                                   ext-emailrelay-cfg-dir))
    (unless (get-process "emailrelay-client")
      (rdf-emailrelay-send-email ext-emailrelay-program
                                 ext-emailrelay-cfg-dir)))
  (defun rdf-send-email-buffer-to-internet ()
    "Send email out to external server"
    (interactive)
    (message-send-and-exit)
    (rdf-send-email))
  :config
  (require 'nnir)
  (setq user-mail-address "kevin.remegame@gmail.com"
        user-full-name "PENG Kevin")
  (setq message-directory (concat ext-emailrelay-cfg-dir "/../gnus/"))
  (setq nnml-directory message-directory)
  (setq gnus-select-method '(nnmaildir "Kevin" (directory message-directory)))
  (setq gnus-secondary-select-methods
        '((nnimap "imap.gmail.com"
                  (nnimap-addrress "imap.gmail.com")
                  (nnimap-server-port 993)
                  (nnimap-stream ssl)
                  (nnimap-authenticator login)
                  (nnir-search-engine imap))))
  (setq nnmail-resplit-incoming t
        nnmail-split-methods 'nnmail-split-fancy)
  ;; document refer: [[info:gnus#Fancy%20Mail%20Splitting][info:gnus#Fancy Mail Splitting]]
  (setq nnmail-split-fancy
        '(| ("from" mail
             (|
              ("from" "kevin.remegame@gmail.com" "SendOut")
              ("from" "\\(njit.pk@163.com\\|.*@cn.bosch.com\\)" "Personal")
              ))
            "Others"))
  ;; make mail list more readable
  ;; http://groups.google.com/group/gnu.emacs.gnus/browse_thread/thread/a673a74356e7141f
  (when window-system
    (setq gnus-sum-thread-tree-indent "  ")
    (setq gnus-sum-thread-tree-root "") ;; "● ")
    (setq gnus-sum-thread-tree-false-root "") ;; "◯ ")
    (setq gnus-sum-thread-tree-single-indent "") ;; "◎ ")
    (setq gnus-sum-thread-tree-vertical        "│")
    (setq gnus-sum-thread-tree-leaf-with-other "├─► ")
    (setq gnus-sum-thread-tree-single-leaf     "╰─► "))
  (setq gnus-summary-line-format
        (concat
         "%0{%U%R%z%}"
         "%3{│%}" "%1{%d%}" "%3{│%}" ;; date
         "  "
         "%4{%-20,20f%}"               ;; name
         "  "
         "%3{│%}"
         " "
         "%1{%B%}"
         "%s\n"))
  (setq gnus-summary-display-arrow t)
  ;; don't hidden any mail in INBOX
  (setq gnus-parameters
        '((".*"
           (display . all)
           (gnus-use-scoring nil))))
  (setq gnus-permanently-visible-groups "INBOX")
  ;; newest email first
  (setq gnus-thread-sort-functions
        '(gnus-thread-sort-by-most-recent-number))
  (setq gnus-activate-level 1) ;;this will fast INBOX open
  ;; send mail
  (setq smtpmail-smtp-server "smtp.gmail.com"
        smtpmail-smtp-service 587
        gnus-ignored-newsgroups "^to\\.\\|^[0-9. ]+\\( \\|$\\)\\|^[\"]\"[#'()]")

  (setq message-send-mail-function 'smtpmail-send-it
        smtpmail-starttls-credentils '(("localhost" 25 "kevin.remegame@local.gmail.com" nil))
        smtpmail-auth-credentials '(("localhost" 25 "kevin.remegame@local.gmail.com" nil))
        smtpmail-default-smtp-server "localhost"
        smtpmail-smtp-server "localhost"
        smtpmail-smtp-service 25
        smtpmail-local-domain "local.gmail.com")
  (setq send-mail-function 'smtpmail-send-it)
  (setq smtpmail-smtp-server "127.0.0.1")
  (setq smtpmail-smtp-service 25)
  (setq user-mail-address "kevin.remegame@gmail.com")

  ;; hide html mails
  (setq mm-discouraged-alternatives
        '("text/html" "text/richtext")
        mm-automatic-display
        (-difference mm-automatic-display '("text/html" "text/enriched" "text/richtext")))

  ;; hide quoted text
  (setq gnus-treat-hide-citation t)

  (setq gnus-use-adaptive-scoring t)
  (setq gnus-default-adaptive-score-alist
        '((gnus-unread-mark)
          (gnus-ticked-mark (subject 10))
          (gnus-killed-mark (subject -5))
          (gnus-catchup-mark (subject -1))))

  (setq mm-verify-option 'always)
  (setq mm-decrypt-option 'always)
  (setq mm-encrypt-option 'guided)
  (setq gnus-buttonized-mime-types '("multipart/signed"))

  (defun stemacs-switch-close ()
    "Switch window and close it."
    (interactive)
    (progn
      (other-window 1)
      (delete-window)))

  (add-hook 'gnus-group-mode-hook
            (lambda ()
              (progn
                ;;(rdf-send-email) ; start local smtp server
                (define-key gnus-group-mode-map (kbd "n") 'gnus-group-next-group)
                (define-key gnus-group-mode-map (kbd "p") 'gnus-group-prev-group))))
  (add-hook 'gnus-summary-mode-hook
            (lambda ()
              (progn
                (define-key gnus-summary-mode-map (kbd "x") 'stemacs-switch-close)
                (define-key gnus-summary-mode-map (kbd "n") 'next-line)
                (define-key gnus-summary-mode-map (kbd "p") 'previous-line)
                (define-key gnus-summary-mode-map (kbd "<delete>") 'gnus-summary-delete-article)
                (define-key gnus-summary-mode-map (kbd "g") 'gnus-summary-insert-new-articles))))
  (add-hook 'gnus-article-mode-hook
            (lambda ()
              (progn
                (define-key gnus-article-mode-map (kbd "<delete>") 'gnus-summary-delete-article))))
  :bind
  (:map redef-global-key-bindings-high-effort-map
   ("s" . rdf-send-email)
   :map message-mode-map
   ("C-c C-c" . rdf-send-email-buffer-to-internet)
   :map gnus-group-mode-map
   ("M-p" . redef-previous-buffer)
   ("M-n" . redef-next-buffer))
  )
```


#### bbdb <span class="tag"><span class="bbdb">bbdb</span></span> {#bbdb}

```emacs-lisp
(use-package bbdb
  :requires (bbdb-loaddefs)
  :ensure t
  :after (gnus)
  :init
  (setq bbdb-file (concat ext-emailrelay-cfg-dir "../bbdb"))
  :config
  (bbdb-initialize 'gnus 'message)
  (bbdb-mua-auto-update-init 'gnus 'message)
  (setq bbdb-pop-up-window-size 10)
  (setq bbdb-mua-update-interactive-p '(query . create))
  (setq bbdb-file "~/.bbdb"
        bbdb-offer-save 'auto
        bbdb-notice-auto-save-file t
        bbdb-expand-mail-aliases t
        bbdb-canonicalize-redundant-nets-p t
        bbdb-always-add-addresses t
        bbdb-complete-name-allow-cycling t)
  (add-hook
   'gnus-summary-mode-hook
   (lambda ()
     (define-key gnus-summary-mode-map (kbd ";") 'bbdb-mua-edit-field)
     ))
  )
```


#### bbdb-vcard <span class="tag"><span class="bbdb_vcard">bbdb-vcard</span></span> {#bbdb-vcard}

```emacs-lisp
(use-package bbdb-vcard
  :requires (vcard bbdb)
  :ensure t)
```


#### mu4e <span class="tag"><span class="mu4e">mu4e</span></span> {#mu4e}

1.  send mail directly :: `compose-mail` to send email, use `c-c c-a` to add
    attachment
2.  edit mail in org mode :: `org-mime-edit-mail-in-org-mode`
    -   `message-signature` define signature
    -   `mail-personal-alias-file` define file which define email alias,
        use `mail-abbrev-insert-alias` insert alias
3.  htmlize mail and send :: `org-mime-htmlize`

<!--listend-->

```emacs-lisp
(with-linux
 (use-package mu4e
   ;; if not exist this dir, try 'sudo apt-get install mu4e'
   :load-path "/usr/share/emacs/site-lisp/mu4e/"
   :init
   (defun offlineimap-get-password (host port)
     (require 'netrc)
     (let* ((netrc (netrc-parse (expand-file-name "~/.authinfo.gpg")))
            (hostentry (netrc-machine netrc host port port)))
       (when hostentry (netrc-get hostentry "password"))))
   :config
   (setq mail-user-agent 'mu4e-user-agent)
   (setq mu4e-maildir (concat rdf_email "/gmail/offlineimap/"))
   (setq mu4e-get-mail-command "offlineimap")
   (setq mu4e-update-interval nil)
   (setq mu4e-sent-folder "/Sent")
   (setq mu4e-drafts-folder "/Drafts")
   (setq mu4e-trash-folder "/Trash")
   (setq mu4e-refile-folder "/Archive")
   (require 'mu4e-contrib)
   (setq mu4e-html2text-command 'mu4e-shr2text)
   (add-hook 'mu4e-view-mode-hook
             (lambda ()
               (local-set-key (kbd "<tab>") 'shr-next-link)
               (local-set-key (kbd "<backtab>") 'shr-previous-link)))
   (setq mu4e-view-show-images t)

   ;; SMTP setup
   (setq sendmail-program "msmtp")
   (setq message-send-mail-function 'message-send-mail-with-sendmail
         smtpmail-stream-type 'starttls
         starttls-use-gnutls t)
   ;; Personal info
   (setq user-full-name "PENG Kevin")
   (setq user-mail-address "kevin.remegame@gmail.com")
   ;; gmail setup
   (setq smtpmail-smtp-server "smtp.gmail.com")
   (setq smtpmail-smtp-service 587)
   (setq smtpmail-smtp-user "kevin.remegame@gmail.com")

   (setq mu4e-compose-signature "Best Regards.")
   (setq mu4e-maildir-shortcuts
         '(("/INBOX" . ?i)
           ("/Sent" . ?s)
           ("/Trash" . ?t)
           ("/Drafts" . ?d)
           ("/Archive" . ?a)
           ("/Waiting" . ?w)
           ))

   (add-to-list 'mu4e-bookmarks
                (make-mu4e-bookmark
                 :name "Three days ago"
                 :query "date:3d..now"
                 :key ?q))

   :bind*
   (:map redef-global-key-bindings-mail-map
         ("m" . mu4e)
         ("u" . mu4e-update-mail-and-index)
         ("i" . mail-abbrev-insert-alias)
         ("a" . mml-attach-file) ;;attach outside message
         ("A" . mail-attach-file) ;;attach inside message
         ("s" . compose-mail) ; send email
         )
   ))
```


### cmake <span class="tag"><span class="cmake">cmake</span></span> {#cmake}

cmake-mode exist in cmake source code.

```emacs-lisp
(use-package cmake-mode
  :demand t
  :load-path "~/.emacs.d/ext/cmake/"
  :config
  (add-hook 'cmake-mode-hook
            (lambda ()
              (r-company-gen-local-backends
               '(company-cmake))))
  )
```


### rss <span class="tag"><span class="rss">rss</span></span> {#rss}


#### elfeed <span class="tag"><span class="elfeed">elfeed</span></span> {#elfeed}

```emacs-lisp
(use-package elfeed
  :ensure t
  :init
  (defun r-elfeed-update ()
    (interactive)
    (let ((url-queue-timeout 30))
      (setq elfeed-curl-extra-arguments (if ext-proxy-used
                                            (assoc "https" url-proxy-services)
                                          elfeed-curl-extra-arguments))

      (when elfeed-curl-extra-arguments
        (setq url-using-proxy (cdr elfeed-curl-extra-arguments))

        (setq elfeed-curl-extra-arguments
              (list  "-x" (cdr elfeed-curl-extra-arguments))))
      (elfeed)
      (elfeed-update)))
  :config
  ;; to avoid elfeed too slow if too many news
  (setq elfeed-search-filter "@15-days-ago +unread")

  :bind
  (:map redef-global-key-bindings-high-effort-map
        ("r" . r-elfeed-update))
  )
  ;;
  ;; usage:
  ;; h : help
  ;; S : filter, + TAG to filter tags
  ;;
```


#### elfeed-org <span class="tag"><span class="elfeed">elfeed</span><span class="org">org</span></span> {#elfeed-org}

```emacs-lisp
(use-package elfeed-org
  :ensure t
  :after (elfeed)
  :config
  (elfeed-org)
  (setq rmh-elfeed-org-files (list "~/.emacs.d/redef/rss/elfeed.org")
  ))
```


### gpg <span class="tag"><span class="gpg">gpg</span></span> {#gpg}

```emacs-lisp
(use-package epa
  :ensure t
  :demand t
  :config
  (with-windows-nt
   (custom-set-variables
    (list 'epg-gpg-program ext-gpg-program)
    (list 'epg-gpg-home-directory "c:/Users/redef/AppData/Roaming/gnupg/")
    (list 'epg-gpgconf-program (concat (file-name-directory ext-gpg-program) "gpgconf.exe"))))
  ;; Do not use gpg agent when runing in terminal
  (defadvice epg--start (around advice-epg-disable-agent activate)
    (let ((agent (getenv "GPG_AGENT_INFO"))
          (display (getenv "DISPLAY")))
      (setenv "GPG_AGENT_INFO" nil)
      (setenv "DISPLAY" nil)
      ad-do-it
      (setenv "DISPLAY" display)
      (setenv "GPG_AGENT_INFO" agent)))
  (epa-file-enable)
  )
```


### beacon <span class="tag"><span class="beacon">beacon</span></span> {#beacon}

```emacs-lisp
  (use-package beacon
    :ensure t
    :demand t
    :config
    (beacon-mode 1)
    ;; for after helm popup frame and hidden
    ;; show current cursor when turn back
    (setq beacon-blink-when-focused t)
    (add-to-list 'beacon-dont-blink-commands 'redef-previous-buffer)
    (add-to-list 'beacon-dont-blink-commands 'redef-next-buffer)
)
```


### dired <span class="tag"><span class="dired">dired</span></span> {#dired}

```emacs-lisp
(use-package neotree
  :demand t
  :ensure t
  :init
  (defun r-dir-tree ()
    (interactive)
    (neotree-dir default-directory))
  :bind*
  (:map redef-global-key-bindings-low-effort-map
        ("D" . r-dir-tree)
        ("d" . neotree-toggle)))
```


### lsp-mode <span class="tag"><span class="lsp">lsp</span></span> {#lsp-mode}

For ruby solargraph, no more packaged needed. Lsp-mode has support
lsp-solargraph default, check variables with lsp-solargraph- prefix.
Sometimes need run `solargraph download-core` and `yard gems` to generate document for
installed gems.
For rails support, following the site <https://solargraph.org/guides/rails>
Run `bundle exec solargraph bundle` under project dir.

```emacs-lisp
(setq lsp-keymap-prefix "M-k")
(use-package lsp-mode
  :ensure t
  :demand t
  :hook (
         (ruby-mode . lsp)
         (c++-mode . lsp)
         (c-mode . lsp)
         (haskell-mode . lsp)
         )
  :init
  :config
  (setq gc-cons-threshold 100000000)
  (setq read-process-output-max (* 1024 1024))
  (setq lsp-prefer-capf t)
  (setq lsp-idle-delay 0.500)
  (setq lsp-print-performance t)
  (setq lsp-diagnostic-package :none) ; disable flycheck
  (setenv "SOLARGRAPH_CACHE" (concat ext-tmp-dir ".solargraph/"))
  (setq lsp-solargraph-library-directories
        (list "~/.rbenv/"
              (concat ext-root-program "/lib/ruby/")
              "~/.rvm"
              "~/.gem"
              ))
  )

(use-package lsp-ui
  :ensure t
  :demand t
  :commands lsp-ui-mode
  :config
  (setq lsp-ui-sideline-show-diagnostics nil)
  (setq lsp-ui-sideline-show-hover nil)
  (setq lsp-ui-sideline-show-code-actions nil)
  (setq lsp-ui-sideline-update-mode 'line)
  (setq lsp-ui-sideline-delay 1.0)
  (setq lsp-ui-peek-enable t)
  (setq lsp-ui-peek-show-directory nil)
  (setq lsp-ui-doc-enable nil)
  (setq lsp-ui-doc-delay 1.0)
  (define-key lsp-ui-mode-map [remap xref-find-definitions] #'lsp-ui-peek-find-definitions)
  (define-key lsp-ui-mode-map [remap xref-find-references] #'lsp-ui-peek-find-references)
  )

(use-package helm-lsp
  :ensure t
  :after (helm-mode)
  :demand t
  :commands helm-lsp-workspace-symbol)

(use-package ccls ;for clang
  :ensure t
  :demand t
  :config
  (require 'ccls)
  (with-windows-nt
   (setq ccls-executable "d:/yardf/program/ccls/ccls.exe"))
  )
```


### backward-forward <span class="tag"><span class="navi">navi</span><span class="backward_forward">backward-forward</span></span> {#backward-forward}

```emacs-lisp
(use-package backward-forward
  :ensure t
  :demand t
  :init
  (add-hook 'backward-forward-mode-hook
            (lambda ()
              ;; remove switch-to-buffer tracking, this navi can be done by M-p,M-n
              (advice-remove 'switch-to-buffer #'backward-forward-push-mark-wrapper)
              (advice-remove 'ggtags-find-tag-dwim #'backward-forward-push-mark-wrapper)
              (advice-add 'r-find-definition :before #'backward-forward-push-mark-wrapper)
              (advice-add 'r-find-reference :before #'backward-forward-push-mark-wrapper)
              (advice-add 'r-find-symbol :before #'backward-forward-push-mark-wrapper)
              (advice-add 'r-find-pop-stack :before #'backward-forward-push-mark-wrapper)
              ))
  :config
  (backward-forward-mode 1))
```


### langtool <span class="tag"><span class="langtool">langtool</span></span> {#langtool}

```emacs-lisp
(use-package langtool
  :ensure t
  :demand t
  :config
  (if ext-langtool-program
      (setq langtool-language-tool-server-jar
            (concat
             (file-name-directory ext-langtool-program)
             "/languagetool-server.jar")))
  (setq langtool-default-language "en-US")
  (setq langtool-mother-tongue "en")
  :bind*
  (:map redef-global-key-bindings-flycheck-map
        ("l" . langtool-check)
        ("L" . langtool-check-done)
        ("b" . langtool-correct-buffer)
        ("h" . langtool-show-message-at-point)
        ))
```


### plantuml <span class="tag"><span class="plantuml">plantuml</span></span> {#plantuml}

remove "--illegal-access=deny" from plantuml-java-args if java version &lt;=8

```emacs-lisp
(use-package plantuml-mode
  :ensure t
  :demand t
  :init
  (setq plantuml-jar-path ext-plantuml-program)
  (setq plantuml-default-exec-mode 'jar)
  (setq org-plantuml-jar-path ext-plantuml-program)
  (setq plantuml-java-args '("-Djava.awt.headless=true" "-jar"))
  :config
  (add-to-list 'auto-mode-alist '("\\.plantuml$\\|\\.puml$" . plantuml-mode))
  (add-to-list 'org-src-lang-modes '("plantuml" . plantuml))
  )
```


### haskell <span class="tag"><span class="hashkell">hashkell</span></span> {#haskell}

lsp-haskell server use hls instead of hie, hie only support 8.6.5, for higher
version &gt;= 8.10 not support, so use official HLS instead, this is suggest by
haskell official team.
pandoc setup need `/tmp/` not full, or an error will happen during run
`stack install`
`cabal install haskell-language-server` to install HLS.
Make soft link in `$HOME` for `~/.stack`

```emacs-lisp
(use-package haskell-mode
  :ensure t
  :demand t
  :bind*
  (:map redef-global-key-bindings-haskell-map
        ("e" . haskell-interactive-bring) ; start REPL
        ("l" . haskell-process-load-or-reload)
        ("t" . haskell-process-do-type)
        ("b" . haskell-process-cabal-build) ; build project
        ("d" . haskell-debug)
        ("i" . haskell-process-do-info))
  :config
  (require 'haskell-interactive-mode)
  (require 'haskell-process)
  (setq haskell-completions-complete-operators nil)
  (custom-set-variables
   `(haskell-process-path-stack ext-haskell-stack-program)
   '(haskell-process-type 'stack-ghci)
   '(haskell-process-suggest-remove-import-lines t)
   '(haskell-process-auto-import-loaded-modules t)
   '(haskell-process-log t))
  (add-hook 'haskell-mode-hook 'interactive-haskell-mode)
  (add-hook 'haskell-mode-hook #'lsp)
  (add-hook 'haskell-mode-hook
            (lambda ()
              ;; solve the error:
              ;; The Haskell process `xxx' has died. Restart?
              (set-language-environment 'utf-8)
              ))
  )
(use-package lsp-haskell
  :if ext-haskell-engine-program
  :demand t
  :config
  ;;(setenv "PATH" (concat
  ;;                (getenv "PATH") ";"
  ;;                (r-get-process-output
  ;;                 (concat ext-haskell-stack-program " path --compiler-bin"))))
  :init
  (setq lsp-haskell-process-path-hie ext-haskell-engine-program)
  (setq lsp-haskell-server-path ext-haskell-engine-program)
  (setq lsp-haskell-process-args-hie (list "-d" "-l" (concat (file-name-directory ext-haskell-engine-program)
                                                             "hie.log"))))

(use-package pandoc-mode
  :if ext-haskell-stack-program
  :demand t
  :config
  (setenv "STACK_ROOT" (concat (file-name-directory rdf-pdir) ".stack"))
  (custom-set-variables `(pandoc-binary (concat
                                         (r-get-process-output
                                          (concat ext-haskell-stack-program " path --local-bin"))
                                         "/pandoc")))
  (add-hook 'markdown-mode-hook 'pandoc-mode)
  (add-hook 'pandoc-mode-hook 'pandoc-load-default-settings))
```


### elm <span class="tag"><span class="elm">elm</span></span> {#elm}

elgot

```emacs-lisp
;;(with-eval-after-load 'company
;;  (add-to-list 'company-backends 'company-elm))
;;(add-hook 'elm-mode-hook #'elm-oracle-setup-completion)
```


### python <span class="tag"><span class="python">python</span></span> {#python}

use python to handle data science task.
install following package:

```bash
pip install -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com numpy
pip install -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com pandas
pip install -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com matplotlib
pip install -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com scipy
```

elpy document <https://elpy.readthedocs.io/en/latest/ide.html#command-elpy-shell-toggle-dedicated-shell>
use `elpy-config` to check environments

```emacs-lisp
(use-package pyvenv
  :ensure t
  :demand t
  :bind*
  (:map redef-global-key-bindings-python-map
        ("a" . pyvenv-activate)
        ("A" . pyvenv-deactivate)
        ("n" . pyvenv-create)
        )
  :config
  ;; default prompt venv directory
  (setq pyvenv-default-virtual-env-name "/home/pk/.config/venv/")

  (pyvenv-mode t)
  ;; Set correct Python interpreter
  (setq pyvenv-post-activate-hooks
        (list (lambda ()
                (setq python-shell-interpreter (concat pyvenv-virtual-env "bin/python")))))
  (setq pyvenv-post-deactivate-hooks
        (list (lambda ()
                (setq python-shell-interpreter "python"))))
  (pyvenv-activate (concat pyvenv-default-virtual-env-name "python3")))

(use-package elpy
  :ensure t
  :demand t
  :after (pyvenv)
  :init
  (elpy-enable)
  :bind*
  (:map redef-global-key-bindings-python-map
        ("d" . elpy-pdb-debug-buffer)
        ("s" . elpy-shell-switch-to-shell)
        ("S" . elpy-shell-switch-to-buffer)
        ("T" . elpy-shell-toggle-dedicated-shell)
        ("k" . elpy-shell-set-local-shell)
        ("K" . elpy-shell-kill)
        ("c" . elpy-check)
        ("g" . elpy-goto-definition)
        ("p" . pop-tag-mark)
        ("r" . xref-find-references)
        ("f" . elpy-yapf-fix-code) ;; format code
        )
  :config
  (setq elpy-modules (delq 'elpy-module-flymake elpy-modules))
  (setq elpy-shell-echo-output nil)
  (setq elpy-rpc-python-command "python3")
  (setq python-indent-offset 4)
  (setq python-shell-interpreter "python3")
  (setq elpy-rpc-timeout 2)
  (setq elpy-rpc-virtualenv-path pyvenv-virtual-env)
  (setq python-shell-interpreter "ipython"
        python-shell-interpreter-args "-i --simple-prompt")
  )
```


### pinyin <span class="tag"><span class="pinyin">pinyin</span></span> {#pinyin}

```emacs-lisp
(use-package posframe
  :ensure t
  :demand t)
(use-package pyim-basedict
  :demand t)
(use-package pyim
  :ensure t
  :demand t
  :after (posframe pyim-basedict)
  :config
  (pyim-basedict-enable)
  (setq default-input-method "pyim")
  (setq pyim-default-scheme 'quanpin)
  (setq-default pyim-english-input-switch-functions
                '(pyim-probe-dynamic-english
                  pyim-probe-isearch-mode
                  pyim-probe-program-mode
                  pyim-probe-org-structure-template))

  (setq-default pyim-punctuation-half-width-functions
                '(pyim-probe-punctuation-line-beginning
                  pyim-probe-punctuation-after-punctuation))

  (pyim-isearch-mode 1)
  (setq pyim-page-tooltip 'posframe)
  (setq pyim-page-length 10)
  (setq pyim-dicts
        (list (list
               :name "sogou"
               :file (concat rdf-fdir "/bext/bins/_local_cache/pyim/sogou.pyim"))))
  :bind*
  (("M-," . pyim-convert-string-at-point)
   ("M-<" . pyim-punctuation-toggle)
   ("M-." . pyim-delete-word-from-personal-buffer)))
```


### rtags <span class="tag"><span class="rtags">rtags</span></span> {#rtags}

code navigation
start rtags server `rdm &`
generate compile database `cmake . -DCMAKE_EXPORT_COMPILE_COMMANDS=1`
index `rc -J .`

```emacs-lisp
(use-package rtags
  :demand t
  :init
  (setq rtags-autostart-diagnostics t)
  :config
  (set-variable 'rtags-path ext-rtags-path)
  (rtags-enable-standard-keybindings redef-global-key-bindings-clang-map)
  )

(use-package company-rtags
  :demand t
  :after (company)
  :init
  (setq rtags-completions-enabled t)
  :config
  (add-to-list 'company-backends 'company-rtags)
  )

(use-package helm-rtags
  :if ext-helm-mode-used
  :after (helm-mode)
)
```


### irony <span class="tag"><span class="cpp">cpp</span><span class="irony">irony</span></span> {#irony}

run `sudo ldconfig /home/pk/program/lib/` in ubuntu to add library for irony-server
code completion

```emacs-lisp
(use-package irony-eldoc
  :demand t
  :config
  (add-hook 'irony-mode-hook #'irony-eldoc))

(use-package irony
  :demand t
  :ensure t
  :config
  (add-hook 'c++-mode-hook 'irony-mode)
  (add-hook 'c-mode-hook 'irony-mode)
  (add-hook 'objc-mode-hook 'irony-mode)
  (add-hook 'irony-mode-hook 'irony-cdb-autosetup-compile-options)
  )

(use-package company-irony-c-headers
  :demand t
  :after (irony))

(use-package company-irony
  :demand t
  :after (irony company-irony-c-headers)
  :config
  (add-to-list 'company-backends '(company-irony-c-headers company-irony)))
```


### cling <span class="tag"><span class="cpp">cpp</span><span class="repl">repl</span><span class="cling">cling</span></span> {#cling}

still not work, this package has some issue not fixed by official

```emacs-lisp
(use-package cling
  :demand nil
  :load-path "~/.emacs.d/ext/inferior-cling/"
  :bind*
  (:map redef-global-key-bindings-clang-map
        ("r" . cling-send-region)
        ("d" . cling-wrap-defun-and-send)))
```


### disablemouse <span class="tag"><span class="mouse">mouse</span></span> {#disablemouse}

Sometimes unintend click a mouse make emacs very slowly.

```emacs-lisp
(use-package disable-mouse
  :demand t
  :config
  (global-disable-mouse-mode))
```


### google-c-style <span class="tag"><span class="c_style">c-style</span></span> {#google-c-style}

```emacs-lisp
(use-package google-c-style
  :demand t
  :config
  (add-hook 'c-mode-common-hook 'google-set-c-style)
  (add-hook 'c++-mode-common-hook 'google-set-c-style)
  )
```


### flycheck <span class="tag"><span class="flycheck">flycheck</span></span> {#flycheck}

```emacs-lisp
(use-package flycheck
  :if t ; report error sometimes
  :demand t
  :config
  (add-hook 'c-mode-hook 'flycheck-mode 1)
  (add-hook 'c++-mode-hook
            (lambda ()
              (setq flycheck-gcc-language-standard "c++11")
              (flycheck-mode 1)))
  )
```


### cmake-ide <span class="tag"><span class="cmake">cmake</span></span> {#cmake-ide}

```emacs-lisp
(with-linux
 (use-package cmake-ide
   :if nil
   :demand nil
   :config
   (cmake-ide-setup)))
```


### clang-format <span class="tag"><span class="clang_format">clang-format</span></span> {#clang-format}

setup clang-format command `sudo apt-get install clang-format`
create google style format `=clang-format -style=google -dump-config > .clang-format`

```emacs-lisp
(use-package clang-format
  :ensure t
  :demand t
  :bind*
  (:map redef-global-key-bindings-clang-map
        ("f" . clang-format-buffer)
        ("c" . compile)
        ("g" . gud-gdb))
  )
```


### dap-mode <span class="tag"><span class="dap">dap</span></span> {#dap-mode}

use `gdb` command to debug cpp instead, dap-mode is a vscode plugin.

```emacs-lisp
;; (use-package dap-mode
;;   :defer
;;   :ensure t
;;   :after (lsp-mode)
;;   :config
;;   (require 'dap-lldb)
;;   )
```


### org-roam <span class="tag"><span class="roam">roam</span></span> {#org-roam}

```emacs-lisp
(use-package org-roam
  :if t ; enable this mode when know how to use roam
  :ensure t
  :after org
  :demand t
  :init
  (setq org-roam-v2-ack t)
  ;; :hook
  ;; (after-init . org-roam-mode)
  :bind
  (
   :map redef-global-key-bindings-org-agenda-map
   ("r" . org-roam-buffer-toggle)
   ("f" . org-roam-node-find)
   ("i" . org-roam-node-insert)
   ("s" . org-roam-db-sync)
   ("t" . org-roam-tag-add)
   ("A" . org-roam-alias-add)
   ("E" . rdf-export-roam-to-hugo)
   ("C" . org-lint)
   :map org-roam-dailies-map
   ("D" . org-roam-dailies-capture-date)
   ("d" . org-roam-dailies-goto-date)
   ("Y" . org-roam-dailies-capture-yesterday)
   ("y" . org-roam-dailies-goto-yesterday)
   ("Q" . org-roam-dailies-capture-today)
   ("q" . org-roam-dailies-goto-today)
   ("T" . org-roam-dailies-capture-tomorrow)
   ("t" . org-roam-dailies-goto-tomorrow)
   ("n" . org-roam-dailies-goto-next-note)
   ("p" . org-roam-dailies-goto-previous-note)
   )
  :bind-keymap*
  ("M-q" . org-roam-dailies-map)
  :config
  ;; roam
  (setq org-roam-directory (concat (file-name-directory rdf-emacs-init-file) "../roam/"))
  (setq org-roam-capture-templates
        '(("d" "default" plain "%?" :if-new
           (file+head "${slug}.org" "#+title: ${title}")
           :unnarrowed t
           )))
  ;; roam-daily
  (require 'org-roam-dailies)
  (setq org-roam-dailies-directory (concat org-roam-directory "daily"))
  (setq org-roam-dailies-capture-templates
        '(("d" "default" entry "* %<%I:%M %p> %?" :if-new
           (file+head "%<%Y-%m-%d>.org" "#+title: %<%Y-%m-%d>\n"))))
  ;; db
  (require 'org-roam-db)
  (org-roam-db-autosync-mode)
  )
```


### org-apper {#org-apper}

```emacs-lisp
(use-package org-appear
  :ensure t
  :hook
  (org-mode . org-appear-mode))
```


### pdf-tools <span class="tag"><span class="pdf_tools">pdf-tools</span></span> {#pdf-tools}

```emacs-lisp
(use-package pdf-tools
  :ensure t
  :demand t
  :config
  (pdf-tools-install)
  )
```


### jupyter <span class="tag"><span class="jupyter">jupyter</span></span> {#jupyter}

run `ein:run` to start

```emacs-lisp
(use-package ein
  :ensure t
  :config
  (setq ein:jupyter-default-notebook-directory (concat ext-root-workspace "/jupyter"))
  )
```


### rails <span class="tag"><span class="rails">rails</span></span> {#rails}

slim not maintance, use haml instead.

```emacs-lisp
(use-package slim-mode
  :ensure t)
(use-package haml-mode
  :ensure t
  :init
  (setenv "EDITOR" "emacsclient") ; For rails credentials:edit
  )
(use-package projectile-rails
  :ensure t
  :config
  (projectile-rails-global-mode)
  :bind*
  (
   :map redef-global-key-bindings-ruby-map
        ("M-s" . projectile-rails-server)
        ("M-i" . projectile-rails-console)
        ("M-v" . projectile-rails-find-view)
        ("M-c" . projectile-rails-find-controller)
        ("M-m" . projectile-rails-find-model)
        ("M-h" . projectile-rails-find-helper)
        ("M-t" . projectile-rails-find-spec)
        ("M-l" . projectile-rails-find-layout)
        ("M-f" . projectile-rails-goto-file-at-point)
        ("M-r" . projectile-rails-goto-routes)
        ("M-g" . projectile-rails-mode-goto-map)
   ))
```


### rust <span class="tag"><span class="rust">rust</span></span> {#rust}

if error happen, try run `lsp-workspace-folders-remove` to remove
the wrong workspace. Need update `.toml` file first.
Or remove the file `~/.emacs.d/*lsp-session-*` and open rust file again.
Make soft link in `$HOME` for `~/.cargo`, `~/.rustup`

```emacs-lisp
(use-package rustic
  :ensure t
  :bind* (
          :map redef-global-key-bindings-rust-map
               ("c" . rustic-compile)
               ("n" . rustic-cargo-new)
               ("r" . rustic-cargo-run)
               ("t" . rustic-cargo-test)
               ("b" . rustic-cargo-build)
               ("C" . rustic-cargo-clippy)
               ("R" . lsp-workspace-folders-remove)
               )
  :config
  (require 'lsp-rust)
  (setq lsp-rust-analyzer-server-display-inlay-hints t)
  )

(use-package projectile
  :ensure t
  :config
  ;; fix can't find rust-anasyer workspace issue
  ;; (setq projectile-project-root-files
  ;;     (delete cargo-project-file projectile-project-root-files))
  ;;  should call 'projectile-invalidate-cache' first
  ;;
  ;; use function 'projectile-project-root to debug project identify
  ;;
  (setq projectile-project-root-files-bottom-up
        (delete ".git" projectile-project-root-files-bottom-up))
  (push "Cargo.toml" projectile-project-root-files-bottom-up))

(use-package cargo
  :ensure t
  :after (projectile rustic))


```


### keycast <span class="tag"><span class="keycast">keycast</span></span> {#keycast}

```emacs-lisp
(use-package keycast
  :ensure t
  :bind* ( :map redef-global-key-bindings-low-effort-map
                ("K" . keycast-mode)
                ;; ("O" . keycast-log-mode)
                )
)
```


### protobuf <span class="tag"><span class="protobuf">protobuf</span></span> {#protobuf}

```emacs-lisp
(use-package protobuf-mode
 :config
 (require 'protobuf-mode)
)
```


### sagemath <span class="tag"><span class="sagemath">sagemath</span></span> {#sagemath}

```emacs-lisp
(use-package auto-complete-sage
  :config
  ;; (ac-config-default) ; this will enable ac global
  (setq ac-sage-show-quick-help t)
  (add-hook 'sage-shell:sage-mode-hook 'auto-complete-mode)
  (add-hook 'sage-shell:sage-mode-hook 'ac-sage-setup)
  (add-hook 'sage-shell-mode-hook 'ac-sage-setup))

(use-package sage-shell-mode
  :config
  (setq sage-shell:sage-executable
        (concat rdf-pdir "/mambaforge/envs/sage/bin/sage"))
  (setq sage-shell:input-history-cache-file
        "~/.emacs.d/.sage_shell_input_history")
  (sage-shell:define-alias)
  (add-hook 'sage-shell-mode-hook #'eldoc-mode)
  (add-hook 'sage-shell:sage-mode-hook #'eldoc-mode)
  (add-hook 'sage-shell-after-prompt-hook #'sage-shell-view-mode)
  :bind*
  (
   :map redef-global-key-bindings-sagemath-map
    ("g" . sage-shell:run-sage)
   :map ac-completing-map
   ("C-n" . ac-next)
   ("C-p" . ac-previous)))

(use-package ob-sagemath
  :config
  ;; Ob-sagemath supports only evaluating with a session.
  (setq org-babel-default-header-args:sage '((:session . t)
                                             (:results . "output")))

  ;; C-c c for asynchronous evaluating (only for SageMath code blocks).
  (with-eval-after-load "org"
    (define-key org-mode-map (kbd "C-c c") 'ob-sagemath-execute-async))

  ;; Do not confirm before evaluation
  (setq org-confirm-babel-evaluate nil)

  ;; Do not evaluate code blocks when exporting.
  (setq org-export-babel-evaluate nil)

  ;; Show images when opening a file.
  (setq org-startup-with-inline-images t)

  ;; Show images after evaluating code blocks.
  (add-hook 'org-babel-after-execute-hook 'org-display-inline-images))
```


### latex <span class="tag"><span class="latex">latex</span></span> {#latex}

```emacs-lisp
(use-package tex
  :ensure auctex
  :bind*
  (:map redef-global-key-bindings-org-agenda-map
        ("v" . org-latex-preview)))

(use-package company-auctex)

(use-package org-fragtog
  :after org
  ;; this auto-enables it when you enter an org-buffer, remove if you do not want this
  :hook (org-mode . org-fragtog-mode)
  :config
  ;; scale size of latex formular
  (plist-put org-format-latex-options :scale 2)

  ;;; https://emacs-china.org/t/org-mode-latex-mode/22490

  ;; Vertically align LaTeX preview in org mode
  (defun my-org-latex-preview-advice (beg end &rest _args)
    (let* ((ov (car (overlays-at (/ (+ beg end) 2) t)))
           (img (cdr (overlay-get ov 'display)))
           (new-img (plist-put img :ascent 95)))
      (overlay-put ov 'display (cons 'image new-img))))
  (advice-add 'org--make-preview-overlay
              :after #'my-org-latex-preview-advice)

  ;; from: https://kitchingroup.cheme.cmu.edu/blog/2016/11/06/
  ;; Justifying-LaTeX-preview-fragments-in-org-mode/
  ;; specify the justification you want
  (plist-put org-format-latex-options :justify 'right)

  (defun eli/org-justify-fragment-overlay (beg end image imagetype)
    (let* ((position (plist-get org-format-latex-options :justify))
           (img (create-image image 'svg t))
           (ov (car (overlays-at (/ (+ beg end) 2) t)))
           (width (car (image-display-size (overlay-get ov 'display))))
           offset)
      (cond
       ((and (eq 'center position)
             (= beg (line-beginning-position)))
        (setq offset (floor (- (/ fill-column 2)
                               (/ width 2))))
        (if (< offset 0)
            (setq offset 0))
        (overlay-put ov 'before-string (make-string offset ? )))
       ((and (eq 'right position)
             (= beg (line-beginning-position)))
        (setq offset (floor (- fill-column
                               width)))
        (if (< offset 0)
            (setq offset 0))
        (overlay-put ov 'before-string (make-string offset ? ))))))
  (advice-add 'org--make-preview-overlay
              :after 'eli/org-justify-fragment-overlay)

  ;; from: https://kitchingroup.cheme.cmu.edu/blog/2016/11/07/
  ;; Better-equation-numbering-in-LaTeX-fragments-in-org-mode/
  (defun org-renumber-environment (orig-func &rest args)
    (let ((results '())
          (counter -1)
          (numberp))
      (setq results (cl-loop for (begin .  env) in
                             (org-element-map (org-element-parse-buffer)
                                 'latex-environment
                               (lambda (env)
                                 (cons
                                  (org-element-property :begin env)
                                  (org-element-property :value env))))
                             collect
                             (cond
                              ((and (string-match "\\\\begin{equation}" env)
                                    (not (string-match "\\\\tag{" env)))
                               (cl-incf counter)
                               (cons begin counter))
                              ((and (string-match "\\\\begin{align}" env)
                                    (string-match "\\\\notag" env))
                               (cl-incf counter)
                               (cons begin counter))
                              ((string-match "\\\\begin{align}" env)
                               (prog2
                                   (cl-incf counter)
                                   (cons begin counter)
                                 (with-temp-buffer
                                   (insert env)
                                   (goto-char (point-min))
                                   ;; \\ is used for a new line. Each one leads
                                   ;; to a number
                                   (cl-incf counter (count-matches "\\\\$"))
                                   ;; unless there are nonumbers.
                                   (goto-char (point-min))
                                   (cl-decf counter
                                            (count-matches "\\nonumber")))))
                              (t
                               (cons begin nil)))))
      (when (setq numberp (cdr (assoc (point) results)))
        (setf (car args)
              (concat
               (format "\\setcounter{equation}{%s}\n" numberp)
               (car args)))))
    (apply orig-func args))
  (advice-add 'org-create-formula-image :around #'org-renumber-environment)
  )

;; fast math input
(use-package cdlatex
  :config
  (add-hook 'LaTeX-mode-hook #'turn-on-cdlatex)   ; with AUCTeX LaTeX mode
  (add-hook 'latex-mode-hook #'turn-on-cdlatex)   ; with Emacs latex mode
  :bind*
  (:map redef-global-key-bindings-org-agenda-map
        ("m" . cdlatex-mode)) ;; for edit math formular
  )
```


### chatgpt <span class="tag"><span class="chatgpt">chatgpt</span></span> {#chatgpt}

```emacs-lisp
(use-package chatgpt-shell
  :ensure t
  :custom
  ((chatgpt-shell-openai-key
    (lambda ()
      (auth-source-pass-get 'secret "openai-key"))))
  :config
  (setq chatgpt-shell-openai-key (r-get-then-del-env "openai_key"))
  ;; check chatgpt-shell-model-versions
  (setq chatgpt-shell-model-version 5)
  )
```


### hack packages <span class="tag"><span class="hack">hack</span></span> {#hack-packages}


#### google-translate <span class="tag"><span class="google_translate">google-translate</span></span> {#google-translate}

```emacs-lisp
(use-package google-translate ;; must use local, has patch on it
  :ensure nil
  :defer 5
  :load-path "~/.emacs.d/ext/translate/google-translate/"
  :config
  (use-package google-translate-default-ui)
  ;; don't backend-method. google-translate has no async method
  ;;(setq google-translate-backend-method 'curl) ;; default methods has no timeout
  (setq google-translate-default-source-language "en")
  (setq google-translate-default-target-language "zh-CN")
  (with-linux
   (defun google-translate--get-b-d1 () ;; to fix ",tkk:'" issue
     ;; TKK='427110.1469889687'
     (list 427110 1469889687)))
  :bind
  (:map redef-global-key-bindings-high-effort-map
        ("t" . google-translate-at-point)
        ("T" . google-translate-at-point-reverse))
  )
```


#### org-mime <span class="tag"><span class="org_mime">org-mime</span></span> {#org-mime}

```emacs-lisp
(use-package org-mime
  :ensure t
  :load-path "~/.emacs.d/ext/email/org-mime/" ; has a hack in this path
  :bind
  (:map redef-global-key-bindings-mail-map
        ("O" . org-mime-org-buffer-htmlize)
        ("o" . org-mime-org-subtree-htmlize)
        ("e" . org-mime-edit-mail-in-org-mode)
        ("h" . org-mime-htmlize)
        )
  :config
  (setq org-mime-export-options '(:section-numbers nil
                                                   :with-toc nil))
  (add-hook 'message-send-hook 'org-mime-confirm-when-no-multipart)
  )
```


### non-melpa packages <span class="tag"><span class="non_melpa">non-melpa</span></span> {#non-melpa-packages}


#### frame-cmds <span class="tag"><span class="frame">frame</span></span> {#frame-cmds}

```emacs-lisp
(use-package frame-fns
  :demand t
  :load-path "~/.emacs.d/ext/frame/framecmds/"
)
(use-package frame-cmds
  :requires (frame-fns)
  :load-path "~/.emacs.d/ext/frame/framecmds/"
  :bind*
  (("M-<down>" . enlarge-frame)
   ("M-<right>" . enlarge-frame-horizontally)
   ("M-<up>" . shrink-frame)
   ("M-<left>" . shrink-frame-horizontally)
   :map redef-global-key-bindings-low-effort-map
   ("W" . r-frame-transparency))
  :config
  (defun r-frame-transparency ()
    (interactive)
    (require 'frame-cmds) ; function increase-frame-transparency not autoloaded
    (increase-frame-transparency 50)
    ))
```


#### bookmark+ <span class="tag"><span class="bookmark_plus">bookmark-plus</span></span> {#bookmark-plus}

```emacs-lisp
(use-package bookmark)
(use-package bookmark+
  :load-path "~/.emacs.d/ext/bookmark-plus/bookmark-plus-master/"
  :ensure nil
  :demand t
  :bind
  (:map redef-global-key-bindings-bookmark-map
        ("l" . list-bookmarks)
        ("s" . bookmark-set)
        ("j" . bookmark-jump)
        ("n" . bmkp-switch-bookmark-file-create)
        ("p" . bmkp-switch-to-last-bookmark-file)))
```


#### dired+ <span class="tag"><span class="dired_plus">dired-plus</span></span> {#dired-plus}

```emacs-lisp
(use-package dired+
  :demand t
  :load-path "~/.emacs.d/ext/dired+/"
  :config
  ;; (diredp-toggle-find-file-reuse-dir 1)
  (diredp-toggle-find-file-reuse-dir -1) ;; not re-use for eyebrowser switch command
  ;; this bindings move to :bind will not work as expected
  )
```


#### asy-mode <span class="tag"><span class="asy">asy</span></span> {#asy-mode}

```emacs-lisp
(if (featurep 'asy-mode)
    (use-package asy-mode
      :if (and ext-asy-bin-dir
               (file-exists-p (concat ext-asy-bin-dir "asy-mode.el")))
      :load-path ext-asy-bin-dir
      :mode ("\\.asy\\'" . asy-mode)
      :config
      (autoload 'asy-mode "asy-mode.el" "Asmptote major mode." t)
      (autoload 'lasy-mode "asy-mode.el" "hybird Asmptote/Latex major mode." t)
      (autoload 'asy-insinuate-latex "asy-mode.el" "Asymptote insinuate LaTeX." t)
      (setq asy-command "asy -globalwrite")
      ))
```


#### w32-registry <span class="tag"><span class="w32_registry">w32-registry</span></span> {#w32-registry}

```emacs-lisp
(use-package w32-registry
  :if ext-proxy-used
  :demand t
  :load-path "~/.emacs.d/ext/w32-registry/"
  :init
  (defun r-auto-setup-proxy ()
    (interactive)
    (with-windows-nt
     (let ((proxy (w32reg-get-ie-proxy-config)))
       (when proxy
         (setq url-proxy-services
               (append
                (mapcar `(lambda (elt) (cons "http" (car elt)))
                        proxy)
                (mapcar `(lambda (elt) (cons "https" (car elt)))
                        proxy)))
         ;; For gnus and many program, this setting is neccecry:
         (setenv "HTTP_PROXY" (cdr (assoc "http" url-proxy-services)))
         (setenv "HTTPS_PROXY" (cdr (assoc "https" url-proxy-services)))
         )))
    (with-linux
     (setq url-proxy-services
           '(("http" . "127.0.0.1:7890")
             ("https" . "127.0.0.1:7890")))
     (setenv "HTTP_PROXY" "127.0.0.1:7890")
     (setenv "HTTPS_PROXY" "127.0.0.1:7890")
     ;; for solargraph, only use http_proxy
     (setenv "http_proxy" (concat "https://"
                                  (getenv "HTTP_PROXY"))
             )))
  :config
  ;;(r-auto-setup-proxy)
  :bind*
  (
   :map redef-global-key-bindings-low-effort-map
        ("x" . r-auto-setup-proxy)))
```


#### telegram <span class="tag"><span class="telegram">telegram</span></span> {#telegram}

run `telega-server-build` to build server if update needed.

```emacs-lisp
(with-linux
 (use-package rainbow-identifiers
   :demand t
   :load-path "~/.emacs.d/ext/telegram/rainbow-identifiers/"
   )
 (use-package telega
   :demand t
   :load-path "~/.emacs.d/ext/telegram/telega.el/"
   :after (rainbow-identifiers)
   :init
   (setq telega-directory (concat ext-tmp-dir ".telega/"))
   :config
   (defun r-start-telegram-gui ()
     (interactive)
     (if (not ext-telegram-gui)
         (message "ext-telegram-gui not defined!")
       (async-shell-command ext-telegram-gui)))
   (setq telega-proxies
      (list
       '(:server "127.0.0.1" :port 7890 :enable t
                 :type (:@type "proxyTypeHttp"))
       '(:server "127.0.0.1" :port 7891 :enable t
                 :type (:@type "proxyTypeSocks5"))
       ))
   :bind* (
           :map redef-global-key-bindings-low-effort-map
           ("T" . r-start-telegram-gui)
           ("t" . telega)
           )))
```


#### flycheck-google-cpplint <span class="tag"><span class="cpplint">cpplint</span></span> {#flycheck-google-cpplint}

```emacs-lisp
(use-package flycheck-google-cpplint
  :demand t
  :after (flycheck)
  :load-path "~/.emacs.d/ext/flycheck-google-cpplint/"
  :config
  (custom-set-variables
   '(flycheck-c/c++-googlelint-executable "~/.emacs.d/ext/flycheck-google-cpplint/cpplint.py"))
  (custom-set-variables
   '(flycheck-googlelint-verbose "3")
   '(flycheck-googlelint-filter "-whitespace,+whitespace/braces")
   '(flycheck-googlelint-root "project/src")
   '(flycheck-googlelint-linelength "120"))
  :bind*
  (:map redef-global-key-bindings-clang-map
        ("C" . flycheck-list-errors)
        )
  )
```


#### org-roam-ui <span class="tag"><span class="roam_ui">roam-ui</span></span> {#org-roam-ui}

```emacs-lisp
(setq rdf-pkg-path-org-roam-ui (concat ext-root-program "/emacs.d/org-roam-ui/"))
(use-package org-roam-ui
  :if nil
  :demand t
  :load-path rdf-pkg-path-org-roam-ui
  :config
  (setq org-roam-ui-sync-theme t
        org-roam-ui-follow t
        org-roam-ui-update-on-save t
        org-roam-ui-open-on-start t)
  :bind* (
          :map redef-global-key-bindings-org-agenda-map
               ("I" . org-roam-ui-mode)
          )
  )
```
