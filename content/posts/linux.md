+++
title = "linux"
author = ["PENG Kevin"]
draft = false
+++

## tips {#tips}


### 重启输入法 {#重启输入法}

fcitx restart &amp;


### 制作启动盘 {#制作启动盘}

使用 ubuntu 系统自带的 `Startup Disk creator`


## ubuntu 24.04 {#ubuntu-24-dot-04}


### SouGou 输入法的安装 {#sougou-输入法的安装}

ubuntu 24.04 搜狗输入法安装步骤：

在系统中添加中文语言：
打开 LanguageSupport

安装 fcitx 输入法框架：
sudo apt install fcitx
sudo apt install --fix-broken
sudo apt-get update

卸载 ibus 输入法：
sudo apt purge ibus

安装 deb 包：
sudo dpkg -i \*.deb

安装依赖：
sudo apt install libqt5qml5 libqt5quick5 libqt5quickwidgets5 qml-module-qtquick2
sudo apt install libgsettings-qt1


### Ruby 的安装 {#ruby-的安装}

ubuntu 24.04 中使用 ruby3.x，因为 openSSL 3.x 删除
RSA_SSLV23_PADDING removed in OpenSSL 3.x SWI-Prolog/packages-ssl#160
Closed ，旧的 ruby2.x 由于 ssl 的问题会将编译不过。

安装完 ruby3.x 的需要给其换源，不然装本地 local 的 gem 也卡半天，暂时找不到其它 workaround 的办法


### Git lfs server 的安装 {#git-lfs-server-的安装}

lfs-test-server 必须使用 go 的 1.4.7 的版本，用高版本的会出现段错误。

git lfs pull -I &lt;filename&gt;，拉取指定文件

git lfs fetch 时，有些 bin 文件会找不到，不知是哪些文件，需要清理一下仓库


### Emacs 的安装 {#emacs-的安装}

Emacs 版本(&gt;=28.1)：
否则会报错 variably modified ‘sigsegv_stack’ at file scope，
据说是因为 libsigsegv 2.6 through 2.8 有 bug。

交换 caplock 和 left-ctrl 键位
sudo vim /usr/share/X11/xkb/keycodes/evdev
交换 &lt;CAPS&gt; 和 &lt;LCTL&gt; 后面的数字


### 备份 firefox 的配置 {#备份-firefox-的配置}

打开 `about:support` 里面的 `Profile Directory`, 对应的目录就是配置文件目录


### 添加启动快捷键 {#添加启动快捷键}


#### bash {#bash}

对应命令为  `gnome-terminal`


#### rdf-emacs {#rdf-emacs}

对应命令为 `<ruby-full-path> <load.yml full-path>`
注意必须传入 `load.yml` 文件完整路径


### Ubuntu 下按下 "ctr+;" 后总是提示 "Select to paste" {#ubuntu-下按下-ctr-plus-后总是提示-select-to-paste}

这是 fctix 默认按键绑定，在输入法配置 -&gt; Addon -&gt; Clipboard 中
将其重新配置后(选中 ctr+; , 然后按下 esc, 删除配置)，重启 fcitx
`pkill fcitx && fcitx-configtool`


### 安装配置 samba 服务 {#安装配置-samba-服务}

1.  `sudo apt install samba nautilus-share -y`
2.  添加用户 [用户和权限管理]({{< relref "bash#用户和权限管理" >}})
3.  配置 samba
    1.  `sudo systemctl enable --now smbd`
    2.  `sudo smbpasswd -a <user>`
    3.  `sudo chown <user>:<group> <samba_share_dir>`
    4.  在配置文件 /etc/samba/smb.conf 中增加以下配置
        ```cfg
        [<_share_folder>]
           path = /home/<_share_folder>
           available = yes
           valid users = @<user_group> @root
           read only = no
           writeable=yes
           browseable=yes
           public = yes
           guest ok = no
           create mask = 0755
        ```
    5.  `sudo systemctl restart smbd`
