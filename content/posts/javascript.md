+++
title = "*javascript"
author = ["PENG Kevin"]
draft = false
+++

## 语法 {#语法}


## 库管理工具 {#库管理工具}


### nodejs {#nodejs}

setup

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```


### yarn {#yarn}

setup

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn
```
