+++
title = "nodejs"
author = ["PENG Kevin"]
draft = false
+++

## install {#install}

```bash
# install nodejs
# https://askubuntu.com/questions/426750/how-can-i-update-my-nodejs-to-the-latest-version
curl -fsSL https://deb.nodesource.com/setup_current.x | sudo -E bash -
sudo apt-get install -y nodejs
# install yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install yarn
```
