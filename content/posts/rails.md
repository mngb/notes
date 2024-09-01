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
`bin/rails db:migrate`


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


### sidekiq {#sidekiq}


#### setup and run {#setup-and-run}

1.  setup `redis`
    ```bash
    sudo add-apt-repository ppa:redislabs/redis
    sudo apt-get install redis  #setup redis version >= 6+
    sudo systemctl restart redis.service
    ```
2.  run `bundle exe sidekiq`


#### configure {#configure}

1.  run `rails g sidekiq:job <job_name>` create job
2.  edit job file `perform` function
3.  call `<jobClass>.perform_async`


#### tips {#tips}

`Job.perform_async` 返回的 job_id 是一个字符串，不能当成整形处理！


### action cable {#action-cable}


## 最佳实践 {#最佳实践}


### migration 操作 {#migration-操作}

查看当前数据库迁移状态
: `rake db:migrate:status`

升级降级数据库到指定版本
: -   **升级:** `rake db:migrate:up VERSION=20240605100428`
    -   **降级:** `rake db:migrate:down VERSION=20240605100428`

console 中执行迁移，一般在 migrate 命令出现执行问题时才直接操作
    `require './db/migrate/20240620102654_add_session_id_to_tasks'`
    然后再创建对象后调用相应方法。


### working with javascript {#working-with-javascript}

<https://stackoverflow.com/questions/46534739/how-to-use-javascript-in-ruby-on-rails>
在 `application.js` 文件中添加相应包。


### 编写路由 {#编写路由}

root
:


resources
:


resource
:


scope
:


module
:


member
:


collection
:


### 编写测试 {#编写测试}

-   可以快速迭代
-   能熟悉工作原理


### 编写 model {#编写-model}

1.  创建一个 model
    `rails g model <TableName> field:type ...`
2.  使 model 生效
    `rails db:migrate`
3.  修改 model
    生成一个迁移 `rails g migration <migration_name> field:type`
    其中 migration_name 可以是
    -   add_xxx_to_yyy
    -   remove_xxx_from_yyy
    -   create_xxx
    -   xxx join_table yyy


### rails 启动流程 {#rails-启动流程}


## tips {#tips}


### Webpacker::Manifest::MissingEntryError - Webpacker can't find application.js {#webpacker-manifest-missingentryerror-webpacker-can-t-find-application-dot-js}

run `bin/rails webpacker:install`


### \`verify_server_version': Error connecting to Spring server (RuntimeError) {#verify-server-version-error-connecting-to-spring-server--runtimeerror}

run `spring stop`


### mailer {#mailer}

为 gmail 重新生成应用专用密码，会解决连接超时的问题，目前还不知道具体原因。
另外新登录的设备要在 gmail 中确认本人所为，不然好像第二次连接会被屏蔽。


#### warning: already initialized constant Net::ProtocRetryError {#warning-already-initialized-constant-net-protocretryerror}

Rails 6.1.7.2 升级 gem mail 后会出现，将 mail 从 2.8+ 降级到  2.7+ 可以消除


### emacs 项目中自动补全 {#emacs-项目中自动补全}

javascript 项目
: 打开顶层 `application.js` 执行 `lsp` 即可。

ruby 项目
:


## 参考文档 {#参考文档}

官方手册
: <https://guides.rubyonrails.org/index.html>

入门文档
: [rails5_tutorial.pdf](/ox-hugo/rails5_tutorial.pdf)

手册
: [rails5.pdf](/ox-hugo/rails5.pdf)

敏捷开发基于 Rails4
: [AgileWebDevelopment_Rails_4thEdition.pdf](/ox-hugo/AgileWebDevelopment_Rails_4thEdition.pdf)
