+++
title = "substrate"
author = ["PENG Kevin"]
draft = false
+++

## install {#install}

-   install dependency
    `apt-get update`
    `sudo apt install --assume-yes git clang curl libssl-dev llvm libudev-dev make protobuf-compiler`
-   install [nodejs]({{< relref "nodejs.md" >}})
-   install [rust]({{< relref "rust.md" >}})
    config rust ::
    ```bash
    rustup default stable
    rustup update
    rustup update nightly
    rustup target add wasm32-unknown-unknown --toolchain nightly
    rustup show
    rustup +nightly show
    ```


## build {#build}


### build node-template {#build-node-template}

```bash
git clone https://github.com/substrate-developer-hub/substrate-node-template
cd substrate-node-template
cargo build --release
```


### build front-end-template {#build-front-end-template}

```bash
git clone https://github.com/substrate-developer-hub/substrate-front-end-template
cd substrate-front-end-template
yarn install
yarn start
# visit http://localhost:8000
```


## run {#run}


### node-template {#node-template}

1.  start node-template
    ```bash
    ./target/release/node-template --dev
    ```
2.  start front-end-template
    ```bash
    yarn start
    ```


### setup trusted node {#setup-trusted-node}


#### generate keys {#generate-keys}

<!--list-separator-->

-  generate key for block product

    ```bash
    ./target/release/node-template key generate --scheme Sr25519 --password-interactive
    ```

    generate key info like this:

    ```text
    Secret phrase:  pig giraffe ceiling enter weird liar orange decline behind total despair fly
    Secret seed:       0x0087016ebbdcf03d1b7b2ad9a958e14a43f2351cd42f2f0a973771b90fb0112f
    Public key (hex):  0x1a4cc824f6585859851f818e71ac63cf6fdc81018189809814677b2a4699cf45
    Account ID:        0x1a4cc824f6585859851f818e71ac63cf6fdc81018189809814677b2a4699cf45
    Public key (SS58): 5CfBuoHDvZ4fd8jkLQicNL8tgjnK8pVG9AiuJrsNrRAx6CNW
    SS58 Address:      5CfBuoHDvZ4fd8jkLQicNL8tgjnK8pVG9AiuJrsNrRAx6CNW
    ```

<!--list-separator-->

-  generate key for block finalize

    this key derive from Sr25519 key.

    ```bash
    ./target/release/node-template key inspect --password-interactive --scheme Ed25519 "<Sr25519 Secret phrase>"
    ```


#### configure chain spec {#configure-chain-spec}

1.  generate a template
    ```bash
    ./target/release/node-template build-spec --disable-default-bootnode --chain local > specFile.json
    ```
2.  edit `specFile.json`, eg. change name, add predefined SS58 public keys
3.  convert to raw spec, which can be used by node
    ```bash
    ./target/release/node-template build-spec --chain=specFile.json --raw --disable-default-bootnode > specFileRaw.json
    ```


#### configure keys in node {#configure-keys-in-node}

1.  start node using raw chain spec
    ```bash
    ./target/release/node-template \
        --base-path /tmp_disk/node01/ \
        --chain ./specFileRaw.json \
        --port 30333 \
        --ws-port 9945 \
        --rpc-port 9933 \
        --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" \
        --validator \
        --rpc-methods Unsafe \
        --name MyNode01 \
        --password-interactive
    ```
2.  insert block product key into keystore
    ```bash
    ./target/release/node-template key insert --base-path /tmp_disk/node01/ \
                                   --chain specFileRaw.json \
                                   --scheme  Sr25519 \
                                   --suri "<Sr25519 Secret phrase>" \
                                   --password-interactive \
                                   --key-type aura
    ```

3.  insert block finalize key into keystore
    ```bash
    ./target/release/node-template key insert --base-path /tmp_disk/node01/ \
                                   --chain specFileRaw.json \
                                   --scheme  Ed25519 \
                                   --suri "<Sr25519 Secret phrase>" \
                                   --password-interactive \
                                   --key-type gran
    ```
4.  check keystore files
    ```bash
    ls /tmp_disk/node01/chains/local_testnet/keystore
    ```


#### start node {#start-node}

after chain spec and keys for node configuration are finished,
restart node, the block will be able finalized.


### setup contract {#setup-contract}


#### install {#install}

```bash
# sudo apt install binaryen # this will install a low version
#
# download newly version from https://github.com/WebAssembly/binaryen/releases/
# and export PATH=<binaryen_bin_path>:$PATH
#
cargo install cargo-dylint dylint-link
cargo install cargo-contract --force
cargo contract --help
```


#### create and build contract {#create-and-build-contract}

create new contract

```bash
cargo contract new <project_name>
```

change Cargo.toml dependency to correct version,
change `ink_lang_codegen` to correct version

```cfg
ink_primitives = { version = "=3.0.0", default-features = false }
ink_lang_codegen = { version = "=3.0.0", default-features = false }
ink_metadata = { version = "=3.0.0", default-features = false, features = ["derive"], optional = true }
ink_env = { version = "=3.0.0", default-features = false }
ink_storage = { version = "=3.0.0", default-features = false }
ink_lang = { version = "=3.0.0", default-features = false }

scale = { package = "parity-scale-codec", version = "3", default-features = false, features = ["derive"] }
scale-info = { version = "2.1.1", default-features = false, features = ["derive"], optional = true }
```

build contract

```bash
cargo +nightly contract build
```


#### write contract {#write-contract}

use eDSL named ink: <https://github.com/paritytech/ink>


## tools {#tools}


### subkey {#subkey}

<https://docs.substrate.io/reference/command-line-tools/subkey/>
build:

```bash
git clone https://github.com/paritytech/substrate.git
cd substrate
cargo +nightly build --package subkey --release
```

usage:

```bash
# /home/pk/workspace/rdf/rdf/workspace/substrate/substrate/
./target/release/subkey --help
./target/release/subkey inspect-node-key --file <node-key-file>
```


### grafana {#grafana}

install

```bash
sudo apt-get install -y adduser libfontconfig1
wget https://dl.grafana.com/oss/release/grafana_9.2.6_amd64.deb
sudo dpkg -i grafana_9.2.6_amd64.deb
```

start
`sudo systemctl start grafana-server`


### prometheus {#prometheus}

1.  download from <https://prometheus.io/download/>
2.  tar and run
3.  start a node
    `./target/release/node-template --dev`
4.  check metrics data for this node (default port for prometheus is 9615)
    `curl localhost:9615/metrics`
5.  config prometheus.yml
    ```yaml
    scrape_configs:
    ​  - job_name: "substrate_node"
      scrape_interval: 5s
      static_configs:
    ​    - targets: ["localhost:9615"]
    ```
6.  start prometheus
    `promethus --config.file prometheus.yml`
7.  if port already in use error happen
    check by `lsof -i :9090`, my clash app already use this port.
    run `promethus --config.file prometheus.yml --web.listen-address`:&lt;another-not-in-use-port&gt;=


### explorer {#explorer}

<https://polkadot.js.org/apps/#/explorer>


## FAQ {#faq}


### panicked at 'dispatching ink! constructor failed: could not read input' {#panicked-at-dispatching-ink-constructor-failed-could-not-read-input}

不用 firefox, 换一个 chrome 浏览器就好了，暂时还不知具体原因。


### chain type {#chain-type}

链的类型 chainType，常用的如，Development 启动本地单节点网络，Local 启动本地多节点测试网络， Live 为公开测试网络或正式网络


### transaction lifecycle {#transaction-lifecycle}

[transaction_lifecycle](fig/transaction_lifecycle.png)


### basic finalized {#basic-finalized}

```bash
./target/release/node-template --chain=local --base-path /tmp_disk/validator01 --alice --node-key=c12b6d18942f5ee8528c8e2baf4e147b5c5c18710926ea492d09cbd9f6c9f82a --port 30333 --ws-port 9944
./target/release/node-template --chain=local --base-path /tmp_disk/validator02 --bob --node-key=6ce3be907dbcabf20a9a5a60a712b4256a54196000a8ed4050d352bc113f8c58 --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWBmAwcd4PJNJvfV89HwE48nwkRmAgo8Vy3uQEyNNHBox2 --port 30334 --ws-port 9945
```
