+++
title = "*rails"
author = ["PENG Kevin"]
draft = false
+++

## 基本命令 {#基本命令}


### overview command {#overview-command}

rails --help [COMMAND]
: different print depends on current directory

rails about
: show rails environment

bundle help [COMMAND]
:


rails generate scaffold
: full structure demo


### create new project {#create-new-project}

1.  `bundle init`
2.  edit `Gemfile`, add `rails`
3.  install rails by `bundle install --path vendor/bundle --jobs=4`
4.  create new project
    `bundle exec rails new ./ -B --skip-turbolinks --skip-test`
5.  check and edit `Gemfile`
6.  install all dependency by run `bundle install`
7.  run `bin/rails s` to start server


### create controller and view {#create-controller-and-view}

`bin/rails generate controller XxxController index`


### create model {#create-model}

`bin/rails generate model Article title:string body:text`
and run
`bin/rails db:migration`


### open rails console {#open-rails-console}

`bin/rails console`


### setup a gem {#setup-a-gem}

1.  Add gem and version information in `Gemfile`
2.  Run `bundle install`


## 常用包 {#常用包}


### pry-rails {#pry-rails}

rails console 包。安装后可通过 `bin/rails console` 启动。

show create_table DSL
: ? ActiveRecord::ConnectionAdapters::SchemaStatements#create_table, add_column

show query methods
: ls ActiveRecord::QueryMethods


### haml {#haml}

模板引擎 [haml]({{< relref "haml.md" >}})


### devise {#devise}

管理用户登录的包。

1.  在 app 中安装 devise 相关文件
    `bin/rails g devise:install`
2.  在 `config/` 下配置 mailer 的地址和相关配置项
3.  生成对应 view
    `bin/rails g devise:views`
4.  生成 user model
    `bin/rails g devise user`
    `bin/rails db:migrate`


## tips {#tips}


### Webpacker::Manifest::MissingEntryError - Webpacker can't find application.js {#webpacker-manifest-missingentryerror-webpacker-can-t-find-application-dot-js}

run `bin/rails webpacker:install`


### mailer {#mailer}

为 gmail 重新生成应用专用密码，会解决连接超时的问题，目前还不知道具体原因。
另外新登录的设备要在 gmail 中确认本人所为，不然好像第二次连接会被屏蔽。


## 参考文档 {#参考文档}

官方手册
: <https://guides.rubyonrails.org/index.html>

入门文档
: [rails5_tutorial.pdf](/ox-hugo/rails5_tutorial.pdf)

手册
: [rails5.pdf](/ox-hugo/rails5.pdf)

敏捷开发基于 Rails4
: [AgileWebDevelopment_Rails_4thEdition.pdf](/ox-hugo/AgileWebDevelopment_Rails_4thEdition.pdf)
