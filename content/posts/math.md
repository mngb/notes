+++
title = "math"
author = ["PENG Kevin"]
draft = false
+++

## 题目 {#题目}


### 求数列前 n 项和 {#求数列前-n-项和}

题目
: 已知数列 ![](/ltximg/math_ef78d028f6800bad12f521d6046bda2e3f32ec47.png) 前 n 项和记为 ![](/ltximg/math_f8176194a2073ee83a4f4e423ae74a96382229e1.png) , <img src="/ltximg/math_f8176194a2073ee83a4f4e423ae74a96382229e1.png" alt="$a_{2,n}$" /> 前 n 项和记为 <img src="/ltximg/math_9297cfc407c22b9967c9368d11d106b55992bac2.png" alt="$a_{3,n}$" />
    , ... , <img src="/ltximg/math_7c277624c6170a6aaa9c2b273c8dd2a087fd473c.png" alt="$a_{m,n}$" /> 前 n 项和记为 <img src="/ltximg/math_573f6a4cdeb2511908925504c846ca0eb151c285.png" alt="$a_{m+1,n}$" />, 已知 <img src="/ltximg/math_ff7b55afdf5af0adf315e32c357e354c84dc2128.png" alt="$a_{1,n} = n$" /> , 求
    <img src="/ltximg/math_7c277624c6170a6aaa9c2b273c8dd2a087fd473c.png" alt="$a_{m,n}$" /> 的值。

解答
: 猜想：注意到  <img src="/ltximg/math_ff7b55afdf5af0adf315e32c357e354c84dc2128.png" alt="$a_{1,n} = n$" /> , <img src="/ltximg/math_a723f21a0802c97bbe76785726184dc53fd2a917.png" alt="$a_{2,n} = \frac{n(n+1)}{2}$" />,

    <img src="/ltximg/math_04082c57967fd852df00f8a8ac3b14a37d29d8b9.png" alt="$$ a_{3,n} &amp;amp;= \frac{1}{2}[\frac{n(n+1)(2n+1)}{6} + \frac{n(n+1)}{2}]
         \\ &amp;amp;= \frac{n(n+1)(n+2)}{6}
         $$" />
    则 <img src="/ltximg/math_c99384fb0623cd3c889093f25956d27bd014e2ba.png" alt="$a_{m,n} = {{m + n -1}\choose m}$" /> 成立吗？
    证明：对 m 使用数学归纳法，假设猜想在 m 时成立，要证明 m+1 时情形也成立。


    <div id="orga9df019" class="equation-container">
    <span class="equation">
    <img src="/ltximg/math_9dd0ae92c161b4c4f2a5c88a27f951e7e643cbf1.png" alt="\begin{equation*}
    a_{m+1,n} = \sum_{i=1}^{n}{{m + i -1}\choose m} = {{m + n}\choose{m+1}}
    \end{equation*}
    " />
    </span>
    <span class="equation-label">
    1
    </span>
    </div>

    即要证明 [1](#orga9df019) 成立。
    由组合公式：
    <img src="/ltximg/math_1d3712a68b842036564e3019f156820dcd3a5554.png" alt="$$ \binom{m + i - 1}{m} + \binom{m + i - 1}{m + 1} = \binom{m + i}{m+1} $$" />
    [1](#orga9df019) 式可以写成：


    <div id="orge423d54" class="equation-container">
    <span class="equation">
    <img src="/ltximg/math_837f16a02be37a97ca58c24915b91e306fb6f62c.png" alt="\begin{equation*}
    a_{m+1,n} = \binom{m}{m} + \sum_{i=2}^{n}{{m + i -1}\choose m} = \binom{m+1}{m+1} + \sum_{i=2}^{n}{{m + i -1}\choose m}
    \end{equation*}
    " />
    </span>
    <span class="equation-label">
    2
    </span>
    </div>

    [1](#orge423d54) 逐项合并，即得 [1](#orga9df019) . 证毕。


### test {#test}


<div class="equation-container">
<span class="equation">
<img src="/ltximg/math_94196409e949a6a73fb055ecc7755eead9f17f7f.png" alt="   \begin{equation*}
\left\{
\begin{aligned}
x_1+2x_2&amp;amp;=3\\
2x_1-x_2&amp;amp;=1\\
\end{aligned}
\right.
   \end{equation*}
" />
</span>
<span class="equation-label">
3
</span>
</div>
