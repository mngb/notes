+++
title = "*google cloud"
author = ["PENG Kevin"]
draft = false
+++

## command {#command}

refer <https://cloud.google.com/compute/docs/gcloud-compute/tips?hl=zh_cn>


### model {#model}


### create vm {#create-vm}


### login {#login}

`gcloud compute ssh [--zone <zone_name>] --project <project_name> <vm_name>`


### file copy {#file-copy}

copy file
: `gcloud compute scp <vm_name>:<dir_vm> <dir_host>`

copy dir
: `gcloud compute scp --recurse <dir_host>/* <vm_name>:<dir_vm>`


## cost {#cost}


## my vm {#my-vm}


### fil vm {#fil-vm}


### blog vm {#blog-vm}

-   install `ruby`, `rails` and `sinatra`
    1.  `sudo apt-get install ruby`
    2.  `sudo gem install rails`
    3.  `sudo gem install sinatra` as rest api for webApp,phoneApp and desktopApp
-   install `postgresql`
    1.  sudo apt-get install postgresql postgresql-contrib


### cardano vm {#cardano-vm}
