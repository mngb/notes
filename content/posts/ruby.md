+++
title = "ruby 语言笔记"
author = ["PENG Kui"]
tags = ["ruby"]
draft = false
+++

## Ruby 实现 {#ruby-实现}

cruby 第一版本 1995 年 12 月，此外有 jruby (java 平台),
IronRuby (.NET 平台) 实现。


## 常用语法 {#常用语法}


### 正则表达式 {#正则表达式}

named groups
: (?&lt;name&gt;regexp)


### Lambda 表达式和 Proc 对象 {#lambda-表达式和-proc-对象}

Lambda 表达式用 `lambda` 或 `->` 定义。
`Proc` 中 return 将从调用者内部返回，
`Lambda` 内部 return 从自身返回。


## 常用工具 {#常用工具}


### gem {#gem}

push own gem to <https://rubygems.org>
: 1.  use `gem build *.gem` build .gem
    2.  use `gem signin` and enter email and password
    3.  use `gem push *.gem` to push to server


### bundle {#bundle}

`bundle gem <name>` create gem


### rspec {#rspec}

`rspec --init` to init
`rspec .` to run


### pry {#pry}

help
: help

show source
: $ class#method

show document
: ? class#method

list
: ls


### rubocop {#rubocop}

redef config
: <../ruby/.rubocop.yml>

frozen_string_literal
: for ruby performance

Assignment Branch Condition size
: measurement size of methods


### solargraph {#solargraph}

-   setup `gem install solargraph`
-   generate index for all installed gems `yard gems`
    or `yard gems --rebuild`
-   config to generate index auto when install new gems:
    `yard config --gem-install-yri`
-   `solargraph download-core` install ruby version cores
-   `~/.solargraph/cache/` is the cache directory
-   set `lsp-solargraph-use-bundler` to true in bundler project


### sinatra {#sinatra}


#### setup {#setup}

`gem install sinatra`


#### hello world {#hello-world}

```ruby
require 'sinatra'
get '/' do
  'Hello world'
end
```


#### concept {#concept}

<!--list-separator-->

-  routes

    -   带变量 `/w/:name`
    -   带通配符 `/w/*.*`
    -   正则表达式 `%r{xxx}`
    -   自定义 Matcher

    routes 的代码块中返回值可能为：

    -   [status(Int), headers(Hash), response_body(each)]
    -   [status(Int), response_body(each)]
    -   response_body(each)
    -   status(Int)

<!--list-separator-->

-  condtion

    agent
    : user agent

    host_name
    : host name

    provides
    : Http Accept Header

    自定义
    : 举例
        ```ruby
        set(:ConditionName) { |value| condition { rand <= value } }
        ```

<!--list-separator-->

-  template

    有 haml/erb/markdown 等许多。
    可通过 `:locals => HASH` 给模板传递临时变量。
    除了通过 view 文件定义模板，还可通过函数定义：

    ```ruby
    template :name do
      template_string
    end
    ```

<!--list-separator-->

-  filter

    类似 routes 可以带 condition, matcher 也可以是正则表达式。

    -   before
    -   after

<!--list-separator-->

-  预定变量

    params
    : 参数 hash
        -   params['inflat'] 通配符参数数组

    request
        请求对象

    session
        `enable :session` 后存储 session 值对

    logger
        `enable :logging` 后支持日志记录

    env

<!--list-separator-->

-  配置和环境

    -   环境变量 `APP_ENV = production/development/test`
    -   ```ruby
        configure :production do
          set :foo, "bar"
          enable :session
        end
        ```

<!--list-separator-->

-  other

    -   cache_control
    -   public dir
    -   redirect drowser
    -   send_files
    -   access request object
    -   error handle
    -   attachment

<!--list-separator-->

-  参考链接

    <https://github.com/sinatra/sinatra>


### authenticate {#authenticate}

rails use `devise`
sinakra use `warden`


### web server {#web-server}

run `ruby -run -e httpd . -p 8000`


### nokogiri {#nokogiri}


### rbenv {#rbenv}


## 参考文档 {#参考文档}

-   介绍基本语法的书籍 [programming_ruby_4ed.pdf](/ox-hugo/programming_ruby_4ed.pdf)
-   深入实战学习 [ruby-deep-dive.pdf](/ox-hugo/ruby-deep-dive.pdf)
-   编码规范 [README-zhCN.md](/ox-hugo/README-zhCN.md)
