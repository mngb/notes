+++
title = "bash"
author = ["PENG Kevin"]
draft = false
+++

## 命令参数 {#命令参数}

$0：脚本的名称。
$1：第一个位置参数
$#：传递给脚本或函数的参数个数。
$\*：所有位置参数（作为一个单词处理）。
$@：所有位置参数（作为独立的词处理）。


## 控制结构 {#控制结构}


### 条件判断 if {#条件判断-if}

```shell
number = 20
if [ $number -eq 100 ]; then
    echo "100"
elif [ $number -lt 10 ]; then
    echo "x"
else
    echo "xx"
fi
```


### 循环 for/while {#循环-for-while}

```shell
for x in 1 2 3
do
    echo $x
done
```

```shell
count=0
while [ $count -lt 5 ]
do
    count=`expr $count + 1`
    echo $count
done
```


## 参数处理和管道 {#参数处理和管道}


### xargs {#xargs}

通过管道传递参数。

```shell
find ./ -name "*.sh" | xargs ls -l
```


### &gt; &lt; 和 | {#和}

输入重定向 `command < file1`
输出重定向 `command > output_file`
错误重定向 `command 2> output_file`
错误重定向到输出 `command 2>&1`
管道 `cat file1 | more` 上一个命令的输出连接到下一个命令输入


### 参数传递 {#参数传递}

`$0` 自己文件名
`$1,$2,...` 传入的第1,2,...个参数


## 常用命令及参数 {#常用命令及参数}


### 环境变量相关 {#环境变量相关}

-   `export`
-   `which`
-   `whereis`


### 文件操作相关 {#文件操作相关}

`ls mv cp rm touch cat more find chmod mkdir pwd cd tar`

tar
: 压缩 `tar -cxvf <xx.tar.gz> xx`
    解压缩 `tar -xcvf xx.tar.gz`


### 文本处理相关 {#文本处理相关}

`head tail grep wc sed sort uniq tr`


### 查看系统状态 {#查看系统状态}

`top du df uname ps fg bg w`

-   查看端口被哪个进程占用 `lsof -i :55555`
-   查看当前窗口是哪个 tty `tty`
-   查看当前 tty 下的进程 `ps -t $(tty)`


### 系统工具 {#系统工具}

`iperf3` 测试两个端点上下行网速


### 用户和权限管理 {#用户和权限管理}

-   增加用户 `useradd -m -g <group> <user>`
-   设置用户密码 `passwd <user>`
-   修改用户 `usermod`


## 常用技巧 {#常用技巧}


### 输入历史命令 {#输入历史命令}

-   `C-r` 后输入，会根据历史命令自动补全
-   `history` 命令查找
-   `!<number>` 运行历史目录


### session 控制 {#session-控制}

-   `screen` 命令，
-   `screen -S <session-name>` 新建 session
-   `C-a d` 从当前 session detach
-   `screen -r <session-name>` 恢复当前 session 为 `<session-name>`
