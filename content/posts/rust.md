+++
title = "rust"
author = ["PENG Kevin"]
tags = ["PL", "rust"]
draft = false
+++

## 环境安装 {#环境安装}

-   安装 `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
-   调试 `rust-gdb`


## 基本语法 {#基本语法}


### 基本类型 {#基本类型}

i8/i16/i32/i64/i128
u8/u16/u32/u64/u128
f32/f64/bool/char/usize


### 运算符 {#运算符}

类似 c 语言


### 结构体 {#结构体}

```rust
struct TestStr {
    pub fa: i32,
    fb: u32
}
```


### 元组 {#元组}

不同数据类型的元素成组使用元组，相同类型的元素成组使用数组。
定义：

```rust
fn main() {
    let test: (i32, u32) = (1, 2);
    println!("{}", test.0);
}
```

```text
1
```


### 枚举 {#枚举}

```rust
enum Option8 {
    None,
    Some(u8)
}
```


### 模式匹配 {#模式匹配}


#### match {#match}

```rust
fn main() {
    let opt1 = Some(1);
    match opt1 {
        Some(x) => println!("x={}", x),
        _ => println!("none"),
    }
}
```

```text
x=1
```


#### if let {#if-let}

```rust
fn main() {
    let x = Some(1);
    if let Some(y) = x {
        println!("x={}", y);
    }
}
```

```text
x=1
```


### 属性 {#属性}

用 `#[]` 表示，有许多特殊用途。见文档
<https://doc.rust-lang.org/stable/rust-by-example/attribute.html>


## 基本概念 {#基本概念}


### 所有权 {#所有权}


### 生命期 {#生命期}

编译器检查生命期避免悬垂引用


#### 生命期标注 {#生命期标注}


### Trait {#trait}


#### 常用 trait {#常用-trait}


## 阶段目标 {#阶段目标}


### 包管理 {#包管理}

在 `cargo.toml` 中添加依赖：
`<package-name> ="<version>"`


### if/match/for/loop/while 使用 {#if-match-for-loop-while-使用}

```rust
fn main() {
    let mut x = 0;
    loop {
        while x < 2 {
            for i in 0..x {
                println!("{}", i);
            }
            x += 1;
        }
        break;
    }
}
```

```text
0
```


### String/Vec/HashMap 等常用数据结构使用 {#string-vec-hashmap-等常用数据结构使用}

```rust
fn main() {
    let str1 = "Hello".to_string(); //String
    let str2 = String::new();
    let arr1:[i32; 4] = [1,2,3,4];
    let arr2:[i32; 4] = [1i32;4];
    let vec1 = vec![1,2,3];
    let vec2 = Vec::new();
    use std::collections::HashMap;
    let hash1 = HashMap::new();
}
```


### 错误处理和 Option 的使用 {#错误处理和-option-的使用}

```rust
use std::fs::File;
use std::error::Error;
fn main() -> Result<(), Box<dyn Error>> {
    let opt1: Option<&str> = Some("xxx");
    let opt2: Option<&str> = None;
    let f = File::open("test.txt")?;
    let result = File::open("test2.txt");
    match result {
        Ok(f) => println!("no error!"),
        Err(e) => eprintln!("error {}", e),
    }
}
```


### 测试编写 {#测试编写}

在 `fn` 前面加上 `#[test]` 表示该函数为测试函数, 可通过 `cargo test` 运行该
测试。
测试默认关闭 stdout, 需要通过 `cargo test -- --nocapture` 打开输出。


### 文件 i/o 和命令行 {#文件-i-o-和命令行}


#### 从命令行读取输入 {#从命令行读取输入}

```rust
use std::io;
fn main() {
    let str = String::new();
    io::stdin().read_line(&mut str).expect("Read failure");

    let args = std::env::args();
    for arg in args {
        println!("arg is {}", arg);
    }
}
```


#### 读文件 {#读文件}

```rust
use std::io::prelude::*;
use std::fs;

fn main() {
    let str_content = fs::read_to_string("test.txt").unwrap();
    let bin_content = fs::read("test.bin").unwrap();
    let mut buffer:[u8; 6];
    let mut file = fs::File::open("test.txt").unwrap();
    file.read(&mut buffer).unwrap();
}
```


#### 写文件 {#写文件}

```rust
use std::fs;

fn main() {
    fs::write("out.txt", "content").unwrap();
}
```


### 生态 overview {#生态-overview}


#### 常用库及其作用 {#常用库及其作用}

<!--list-separator-->

-  std::env 输入参数解析

    ```rust
    use std::env;

    fn main() {
        let args: Vec<String> = env::args().collect();
        println!("Args is {:?}", args);
    }
    ```

    ```text
    Args is ["target/debug/cargok5wwMM"]
    ```

<!--list-separator-->

-  std::fs 文件操作

<!--list-separator-->

-  std::io

<!--list-separator-->

-  std::path

<!--list-separator-->

-  std::thread

    ```rust
    use std::thread;
    fn main() {
        thread::spawn(move || {
            println!("Thread start");
        });
    }
    ```

    ```text
    error: Could not compile `cargoiWa36D`.
    ```

<!--list-separator-->

-  std::time 和 chrono 时间库

    ```rust
    use chrono::prelude::*;
    use std::time;
    fn main() {
        let now = Local::now();
        let duration = time::Duration::from_millis(1000);
        println!(
            "{}",
            format!(
                "{:4}{:02}{:02}{:02}{:02}",
                now.year(),
                now.month(),
                now.day(),
                now.hour(),
                now.minute() / 10 * 10
            )
        );
    }
    ```

    ```text
    202210222210
    ```


#### Rust 论坛 {#rust-论坛}


### 其它高级特性 {#其它高级特性}


#### 不安全特性 {#不安全特性}

解引用


### 宏 {#宏}


## 参考文档 {#参考文档}

-   rust 圣经翻译版 <https://kaisery.github.io/trpl-zh-cn/>
-   Redef 推荐的语法教材 <https://rustwiki.org/zh-CN/rust-by-example>
