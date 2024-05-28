+++
title = "*hashell"
author = ["PENG Kui"]
draft = false
+++

## environment setup {#environment-setup}


### runtime {#runtime}

1.  setup ghc(haskell compiler) follow <https://www.haskell.org/platform/>
2.  setup stack tool
    -   use `stack ghci` start ghci
    -   use `stack install <package>` install package
    -   -   <https://docs.haskellstack.org/en/stable/README/>
        -   <https://docs.haskellstack.org/en/stable/GUIDE/>
    -   1.  create new project `stack new project-name`
        2.  `cd project-name`
        3.  install dependency `stack setup`
        4.  build project `stack build`
        5.  run your program `stack exec project-exe`

~~3. cabal(haskell package managerm don't use, has some conflict when setup)~~
other tools:

1.  ghci/ghcid/hlint
2.  install Rasterific (a picture draw help to study haskell)
3.  install pandoc (a very useful document converter)
4.  install hoogle (a haskell api search engine)


### emacs {#emacs}

code highlight
: haskell-mode

code completion
: lsp-haskell

code completion server
: haskell-ide-engine
    -   **clone:** git clone <https://github.com/haskell/haskell-ide-engine.git> --recursive
    -   **build:** stack build --stack-yaml stack-8.8.3.yaml

relp
: use `stack ghci`


## haskell language {#haskell-language}


### plan {#plan}


### REPL {#repl}

need set system's coding to utf-8(for Windows need enable 'Beta utf-8 support')
or there may has unknow code be printted.
start repl by use `ghci`,
in `ghci`, use `:?` show the commands.

`:t`
: show types

`:i`
: show information


### typical demo {#typical-demo}


#### hello {#hello}

identiter can only '[a-zA-Z0-9_']'
data type must '^[A-Z]'
other identiter must '^[a-z_]'

```haskell
let x = "hello world"
let y = "hello world2"
putStrLn y
```

```text
hello world2
```


#### basic func {#basic-func}

-   'if' is a expression
-   +, -, \*, /, ^, /=, &amp;&amp;, ||, not
-   succ, min, max, div, pred, _
-   ':', '++', '!!', head, tail,
    init, last, reverse,
    take, drop, length, null,
    minimum, maximum, sum, product,
    elem, cycle, repeat
    [if x&gt;3 then 'a' else 'b' | x &lt;- [2..30], x\*x &lt; 50]
-   fst, snd, zip

<!--listend-->

```haskell

```


### data type {#data-type}

type variable, use `:t fst` can check the type variables
type must can be inference.
use `expression::Type` assign type to expression

class constraint
: use `'=>'`
    function like `'=`'= or `'<'` are have class constraint

typeclass
: Eq, Ord, Show, Read, Bounded, ...
    use `':i <typeclass>'` in ghci to view detail

define
: data(keyword), deriving(keyword),
    value constructor, data record, type parameter,
    type(keyword, same as typedef in C),
    recursive data structure, class constaint,
    class(keyword, define new typeclass) where,
    instance(keyword, make data type of typeclass)where
    :k show kind of a type


### recursion and high order function {#recursion-and-high-order-function}

had better create a `.hs` file and edit, use babel-haskell
will print warning sometimes.
even, odd, filter, map, takeWhile,
let in, case of, $

```haskell
:{
typicalFunc :: (Ord a, Num a) => a -> a -> Ordering
typicalFunc a b
  | a + delta > b = GT
  | a - delta < b = LT
  | otherwise = EQ
  where delta = 2
:}
typicalFunc 3 4
let a=2; b=3 in a * b
:{
case [1,2,3] of [] -> "empty"
                [x] -> "one element"
                [x,_] -> "two elements"
                [x,y,_] -> "three elements"
:}
```

```text
Prelude| Prelude| Prelude| Prelude| Prelude|
<interactive>:30:17-29: warning: [-Woverlapping-patterns]
    Pattern match is redundant
    In a case alternative: [] -> ...

<interactive>:31:17-36: warning: [-Woverlapping-patterns]
    Pattern match is redundant
    In a case alternative: [x] -> ...

<interactive>:32:17-39: warning: [-Woverlapping-patterns]
    Pattern match is redundant
    In a case alternative: [x, _] -> ...
"three element"
```


### haskell project {#haskell-project}


#### language level {#language-level}

modules
: function set, type set and typeclass set
    haskell program must has a 'Main' modules
    as the program's entry

import module
: ```haskell
    import qualified Data.Map (filter) hiding () as M
    ```

standard library
: Data.List, Data.Char, Data.Map, Data.Set, IO
    -   <https://downloads.haskell.org/~ghc/latest/docs/html/libraries/>

IO(System.IO, System.Directory, System.Environment)
: &lt;-, return, getLine, getChar, putStrLn, putStr, putChar,
    getContent, interact, openFile, hGetContents, hClose, withFile,
    readFile, writeFile, appendFile, hGetLine, hGetChar, hPutStr, hPutStrLn,
    hFlush, openTempFile, getCurrentDirectory, renameFile, removeFile,
    getArgs, getProgName, random, pack, unpack, catch


#### use ghc {#use-ghc}

ghc --make your-app.hs


#### use stack {#use-stack}


### funtional programming {#funtional-programming}


## reference {#reference}

short course
: <https://www.seas.upenn.edu/~cis194/fall16/>

short intrudution
: <http://learn.hfm.io/>

more easy
: <http://learnyouahaskell.com/chapters>

report98
: [file:../../../library/Haskell/haskell-98-tutorial.pdf](d:/yardf/rdf/bext/library/Haskell/haskell-98-tutorial.pdf)

report2010
: [file:../../../library/Haskell/haskell2010.pdf](d:/yardf/rdf/bext/library/Haskell/haskell2010.pdf)
