+++
title = "rakefile"
author = ["PENG Kevin"]
draft = false
+++

## 常用语法 {#常用语法}

```ruby
#
# RUN 'rake namespace_name:task_name[p1,p2]' to run
#
desc "namespace desc"
namespace :namespace_name do
  desc "task desc"
  task :task_name, [:param1, :param2] do |t, args|
    puts "#{args[:param1]} #{args[:param2]}"
  end
end

desc "simple task"
task :task1 do
  puts "simple task running"
end
```
