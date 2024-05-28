+++
title = "*git"
author = ["PENG Kevin"]
draft = false
+++

## git 基本原理 {#git-基本原理}


## 常用命令 {#常用命令}


## git 高级功能 {#git-高级功能}


### git lfs {#git-lfs}

为解决大文件托管效率问题而引入。git 中会将大文件替换为一串 Hash 值存储。

1.  `sudo apt-get install git-lfs`
2.  `git lfs install`
3.  `git lfs fetch`


## 托管账户配置 {#托管账户配置}


### gitee {#gitee}

1.  生成密钥。gitee 需要使用 ed25519 才能登录。

<!--listend-->

```bash
ssh-keygen -t ed25519 -C <email>
```

1.  测试连接

<!--listend-->

```bash
ssh -T git@gitee.com
```


### github {#github}

1.  生成 key:

<!--listend-->

```bash
ssh-keygen -t rsa -C <email>
```

1.  在 `~/.ssh/config` 添加如下内容

<!--listend-->

```text
Host github github.com
  HostName github.com
    IdentityFile ~/.ssh/github
    User git
```

注意 `~/.ssh/github` 为生成的 rsa 私钥，
User 必需是 `git`.

1.  Linux 下，还需要运行：

<!--listend-->

```bash
ssh-agent -s
ssh-add ~/.ssh/github
```

将 key 加入系统可识别列表中。

1.  测试连接
    ```bash
    ssh -T git@github.com
    ```
