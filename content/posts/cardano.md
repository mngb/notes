+++
title = "*cardano"
author = ["PENG Kevin"]
draft = false
+++

## knowledge {#knowledge}


## out of techinology {#out-of-techinology}


### develop phase {#develop-phase}

refer <https://roadmap.cardano.org/zh-cn/>


### structure and component {#structure-and-component}

refer <https://docs.cardano.org/explore-cardano/cardano-architecture/overview>
<https://forum.cardano.org/t/iohk/64759>


### ecossystem {#ecossystem}


## build and install {#build-and-install}

1.  install haskell
    `sudo apt-get update -y`
    `sudo apt-get install automake build-essential pkg-config libffi-dev libgmp-dev -y`
    `sudo apt-get install libssl-dev libtinfo-dev libsystemd-dev zlib1g-dev -y`
    `sudo apt-get install make g++ tmux git jq wget libncursesw5 libtool autoconf -y`
    `curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh`
2.  install libsodium
    `git clone https://github.com/input-output-hk/libsodium`
    `cd libsodium`
    `./autogen.sh`
    `./configure`
    `make`
    `sudo make install`
    `export LD_LIBRARY_PATH = "/usr/local/lib:$LD_LIBRARY_PATH"`
    `export PKG_CONFIG_PATH = "/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH"`
3.  install cardano-node
    `git clone https://github.com/input-output-hk/cardano-node.git`
    `cd cardano-node`
    `git fetch --all --recurse-submodules --tags`
    `git tag`
    `git checkout tags/<TAGGED VERSION>`
    `cabal configure --with-compiler=<ghc-8.10.4>`
    `cabal build all`
    `cp -p "$(./scripts/bin-path.sh cardano-node)" ~/.local/bin/`
    `cp -p "$(./scripts/bin-path.sh cardano-cli)" ~/.local/bin/`
    `cardano-cli --version`
    `cardano-node --version`


## configure and boot {#configure-and-boot}


## development {#development}


### contract {#contract}

<https://alpha.marlowe.iohkdev.io/#/>
<https://alpha.marlowe.iohkdev.io/doc/marlowe/tutorials/index.html>
