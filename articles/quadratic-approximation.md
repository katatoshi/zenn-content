---
title: "2回微分可能なら2次近似可能であることについての証明"
emoji: "📝"
type: "tech"
topics:
  - "数学"
  - "最適化"
  - "微分積分"
published: false
---

# はじめに

矢部『工学基礎　最適化とその応用』の2.1節で

> $f$ が $\bm{x}^*$ で2回微分可能ならば，任意のベクトル $\bm{x} \in D$ に対して

$$
\begin{align*}
    f(\bm{x}) = & f(\bm{x}^*) + \sum_{i = 1}^n \frac{\partial f}{\partial x_i} (\bm{x}^*) (x_i - x_i^*) \\
                & + \frac{1}{2} \sum_{i = 1}^n \sum_{j = 1}^n \frac{\partial^2 f}{\partial x_j \partial x_i}(\bm{x}^*) (x_i - x_i^*) (x_j - x_j^*) \\
                & + \left\{ \sum_{i = 1}^n (x_i - x_i^*)^2 \right\} \delta_2(\bm{x}^*; \bm{x} - \bm{x}^*)
\end{align*}
$$

> が成り立つ．ただし，$\delta_2(\bm{x}^*; \cdot): \bm{R}^n \to \bm{R}$ は $\displaystyle \lim_{\bm{x} \to \bm{x}^*} \delta_2(\bm{x}^*; \bm{x} - \bm{x}^*) = 0$ となる関数である．

> $\nabla f(\bm{x})$，$\nabla^2 f(\bm{x})$ の記号を用いれば，式 (2.1) と (2.2) はそれぞれ

$$
\begin{align*}
    f(\bm{x}) = & f(\bm{x}^*) + \nabla f(\bm{x}^*)^\mathrm{T}(\bm{x} - \bm{x}^*) + \|\bm{x} - \bm{x}^*\| \delta_1(\bm{x}^*; \bm{x} - \bm{x}^*) \\
    f(\bm{x}) = & f(\bm{x}^*) + \nabla f(\bm{x}^*)^\mathrm{T}(\bm{x} - \bm{x}^*) \\
                & + \frac{1}{2} (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) + \|\bm{x} - \bm{x}^*\|^2 \delta_2(\bm{x}^*; \bm{x} - \bm{x}^*)
\end{align*}
$$

> と書ける．

と書いてあって，1点で2回微分可能ってだけで2次近似できるんだっけ？　と気になったので自分で証明してみた[^1]．

[^1]:笠原『微分積分学』，杉浦『解析入門』，小平『解析入門』，黒田『微分積分』をざっとみた限り，上の命題は載ってなさそうだった．杉浦と小平についてはヘッセ行列自体載ってない．黒田についてはヘッセ行列も載っていて，上の命題も $f$ が $C^3$-級の場合 (テイラーの公式) は載っていたが，$C^3$-級を仮定しない場合については載っていなかった．

# 微分可能性と記号の定義

以下，微分可能性の定義は笠原『微分積分学』を参考にした．勾配ベクトル，ヘッセ行列の記法は矢部を参考にした．

$D$ を $\bm{R}^n$ の領域 (連結な開集合) とし，$f: D \to \bm{R}$ とする．$f$ が $\bm{x}^* \in D$ で (1回) 微分可能であるとは，あるベクトル $\bm{a} \in \bm{R}$ が存在して

$$
\begin{align}
    & f(\bm{x}) = f(\bm{x}^*) + \bm{a}^\mathrm{T} (\bm{x} - \bm{x}^*) + g(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|} = 0
\end{align}
$$

が成り立つことである．このとき

$$
\bm{a} =
\begin{pmatrix}
    {\displaystyle \frac{\partial f}{\partial x_1}(\bm{x}^*)} \\
    \vdots \\
    {\displaystyle \frac{\partial f}{\partial x_n}(\bm{x}^*)} \\
\end{pmatrix}
$$

である．

ベクトル

$$
\nabla f(\bm{x}) =
\begin{pmatrix}
    {\displaystyle \frac{\partial f}{\partial x_1}(\bm{x})} \\
    \vdots \\
    {\displaystyle \frac{\partial f}{\partial x_n}(\bm{x})} \\
\end{pmatrix}
$$

を $f$ の勾配ベクトルと呼ぶ．勾配ベクトルの記号を用いれば $(1)$ は

$$
\begin{equation}
    f(\bm{x}) = f(\bm{x}^*) + \nabla f(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*) + g(\bm{x})
\end{equation}
$$

と書ける．

微分可能性の定義から，$f$ が $\bm{x}^*$ で微分可能ならば $\bm{x}^*$ で連続であることがわかる．

領域 $D$ の各点で微分可能な関数 $f: D \to \bm{R}$ が $\bm{x}^* \in D$ で2回微分可能であるとは，$f$ のすべての偏導関数 $\frac{\partial f}{\partial x_i}$ $(i = 1, \cdots, n)$ が $\bm{x}^*$ で微分可能，すなわち，すべての $i = 1, \cdots, n$ について

$$
\begin{align}
    & \frac{\partial f}{\partial x_i}(\bm{x}) = \frac{\partial f}{\partial x_i}(\bm{x}^*) + \nabla \frac{\partial f}{\partial x_i}(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*) + g_i(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{g_i(\bm{x})}{\|\bm{x} - \bm{x}^*\|} = 0
\end{align}
$$

が成り立つことである．

行列

$$
\nabla^2 f(\bm{x}) =
\begin{pmatrix}
    \nabla {\displaystyle \frac{\partial f}{\partial x_1}(\bm{x})^\mathrm{T}} \\
    \vdots \\
    \nabla {\displaystyle \frac{\partial f}{\partial x_n}(\bm{x})^\mathrm{T}} \\
\end{pmatrix} =
\begin{pmatrix}
    {\displaystyle \frac{\partial^2 f}{\partial x_1^2}(\bm{x})}            & \cdots &       {\displaystyle \frac{\partial^2 f}{\partial x_n \partial x_1}(\bm{x})} \\
                                                                           & \cdots & \\
    {\displaystyle \frac{\partial^2 f}{\partial x_1 \partial x_n}(\bm{x})} & \cdots & {\displaystyle \frac{\partial^2 f}{\partial x_n^2}(\bm{x})} \\
\end{pmatrix}
$$

を $f$ のヘッセ行列と呼ぶ[^2]．$(4)$ をベクトルにまとめると

[^2]:$\frac{\partial^2 f}{\partial x_j \partial x_i} = \frac{\partial}{\partial x_j}\left(\frac{\partial f}{\partial x_i}\right)$．

$$
\begin{align*}
    \begin{pmatrix}
        {\displaystyle \frac{\partial f}{\partial x_1}(\bm{x})} \\
        \vdots \\
        {\displaystyle \frac{\partial f}{\partial x_n}(\bm{x})} \\
    \end{pmatrix}
    & =
    \begin{pmatrix}
        {\displaystyle \frac{\partial f}{\partial x_1}(\bm{x}^*)} \\
        \vdots \\
        {\displaystyle \frac{\partial f}{\partial x_n}(\bm{x}^*)} \\
    \end{pmatrix}
    +
    \begin{pmatrix}
        {\displaystyle \nabla \frac{\partial f}{\partial x_1}(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*)} \\
        \vdots \\
        {\displaystyle \nabla \frac{\partial f}{\partial x_n}(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*)} \\
    \end{pmatrix}
    +
    \begin{pmatrix}
        g_1(\bm{x}) \\
        \vdots \\
        g_n(\bm{x}) \\
    \end{pmatrix} \\
    & =
        \begin{pmatrix}
        {\displaystyle \frac{\partial f}{\partial x_1}(\bm{x}^*)} \\
        \vdots \\
        {\displaystyle \frac{\partial f}{\partial x_n}(\bm{x}^*)} \\
    \end{pmatrix}
    +
    \begin{pmatrix}
        {\displaystyle \nabla \frac{\partial f}{\partial x_1}(\bm{x}^*)^\mathrm{T}} \\
        \vdots \\
        {\displaystyle \nabla \frac{\partial f}{\partial x_n}(\bm{x}^*)^\mathrm{T}} \\
    \end{pmatrix}
    (\bm{x} - \bm{x}^*)
    +
    \begin{pmatrix}
        g_1(\bm{x}) \\
        \vdots \\
        g_n(\bm{x}) \\
    \end{pmatrix}
\end{align*}
$$

となるので，$\bm{g}(\bm{x}) = (g_1(\bm{x}), \cdots, g_n(\bm{x}))^\mathrm{T}$ として，勾配ベクトルとヘッセ行列を用いれば $(4)$ は

$$
\begin{equation}
    \nabla f(\bm{x}) = \nabla f(\bm{x}^*) + \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) + \bm{g}(\bm{x})
\end{equation}
$$

と書ける．

# 1変数の場合

1変数の場合はロピタルの定理が使えるので簡単に証明できる．

**命題** $\enspace$ 区間 $D = (a, b)$ $(a < x^* < b)$ で定義された関数 $f$ が $D$ 上微分可能で，$x^*$ で2回微分可能であるとする．このとき

$$
\begin{align}
    & f(x) = f(x^*) + f^\prime(x^*) (x - x^*) + \frac{1}{2} f^{\prime\prime}(x^*) (x - x^*)^2 + g(x), \\
    & \lim_{x \to x^*} \frac{g(x)}{(x - x^*)^2} = 0.
\end{align}
$$

**証明** $\enspace$

$$
\begin{align*}
    g(x) = f(x) - f(x^*) - f^\prime(x^*) (x - x^*) - \frac{1}{2} f^{\prime\prime}(x^*) (x - x^*)^2
\end{align*}
$$

とすると，$x \to x^*$ のとき $g(x) \to 0$, $(x - x^*)^2 \to 0$ であり，

$$
\begin{align*}
    \lim_{x \to x^*} \frac{g^\prime(x)}{((x - x^*)^2)^\prime} & = \lim_{x \to x^*} \frac{f^\prime(x) - f^\prime(x^*) - f^{\prime\prime}(x^*) (x - x^*)}{2(x - x^*)} \\
                                                              & = \frac{1}{2} \left(\lim_{x \to x^*} \left(\frac{f^\prime(x) - f^\prime(x^*)}{x - x^*}\right) - f^{\prime\prime}(x^*)\right) \\
                                                              & = \frac{1}{2} \left(f^{\prime\prime}(x^*) - f^{\prime\prime}(x^*)\right) \\
                                                              & = 0
\end{align*}
$$

であるから，ロピタルの定理より

$$
\begin{equation*}
    \lim_{x \to x^*} \frac{g(x)}{(x - x^*)^2} = \lim_{x \to x^*} \frac{g^\prime(x)}{((x - x^*)^2)^\prime} = 0
\end{equation*}
$$

が成り立つ. $\enspace$ (証明終)

# 多変数の場合

多変数の場合はロピタルの定理が使えないので証明がちょっと面倒になる．

$C^1$-級を仮定してよいなら，次の積分公式が使える (証明の一部に問題あり)．

**定理** (積分公式)[^3] $\enspace$ $f(\bm{x})$ が領域 $D$ 上で $C^1$-級なら，

[^3]:笠原 定理 5.17

$$
\begin{equation}
    f(\bm{x}) - f(\bm{x}^*) = \left(\int_0^1 \nabla f(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*).
\end{equation}
$$

ただし，ベクトル値関数の定積分は各成分毎の定積分を成分とするベクトルであり，

$$
\begin{equation*}
    \int_0^1 \nabla f(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt = 
    \begin{pmatrix}
        {\displaystyle \int_0^1 \frac{\partial f}{\partial x_1}(\bm{x}^* + t(\bm{x} - \bm{x}^*))} dt \\
        \vdots \\
        {\displaystyle \int_0^1 \frac{\partial f}{\partial x_n}(\bm{x}^* + t(\bm{x} - \bm{x}^*))} dt \\
    \end{pmatrix}
\end{equation*}
$$

である．

**命題** $\enspace$ 領域 $D$ で定義された関数 $f$ が $C^1$-級で，$x^* \in D$ で2回微分可能であるとする．このとき

$$
\begin{align}
    & f(\bm{x}) = f(\bm{x}^*) + \nabla f(\bm{x}^*)^\mathrm{T}(\bm{x} - \bm{x}^*) + \frac{1}{2} (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) + g(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|^2} = 0.
\end{align}
$$

**証明** $\enspace$ $f$ は $x^*$ で2回微分可能なので

$$
\begin{align*}
    & \nabla f(\bm{x}) = \nabla f(\bm{x}^*) + \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) + \bm{h}(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{\bm{h}(\bm{x})}{\|\bm{x} - \bm{x}^*\|} = \bm{0}
\end{align*}
$$

が成り立つ．積分公式から

$$
\begin{align*}
    & f(\bm{x}) - f(\bm{x}^*) \\
    & = \left(\int_0^1 \nabla f(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \left(\int_0^1 (\nabla f(\bm{x}^*) + t \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) + \bm{h}(\bm{x}^* + t(\bm{x} - \bm{x}^*))) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \left(\nabla f(\bm{x}^*) + \int_0^1 t \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) dt + \int_0^1 \bm{h}(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \nabla f(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*) + \frac{1}{2} (\nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & \qquad + \left(\int_0^1 \bm{h}(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \nabla f(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*) + \frac{1}{2} ((\nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*))^\mathrm{T} \\
    & \qquad + \left(\int_0^1 \bm{h}(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \nabla f(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*) + \frac{1}{2} (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) \\
    & \qquad + \left(\int_0^1 \bm{h}(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*)
\end{align*}
$$

が成り立つ．

$$
\begin{equation*}
    g(\bm{x}) = \left(\int_0^1 \bm{h}(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*)
\end{equation*}
$$

とすると，

$$
\begin{align*}
    \left|\frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|^2}\right|
    & = \frac{\displaystyle \left|\left(\int_0^1 \bm{h}(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right)^\mathrm{T} (\bm{x} - \bm{x}^*)\right|}{\|\bm{x} - \bm{x}^*\|^2} \\
    & = \frac{\displaystyle \left|\sum_{i = 1}^n \left(\int_0^1 h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right) (x_i - x^*_i)\right|}{\|\bm{x} - \bm{x}^*\|^2} \\
    & \leq \frac{\displaystyle \sum_{i = 1}^n \left|\int_0^1 h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*)) dt \right| |x_i - x^*_i|}{\|\bm{x} - \bm{x}^*\|^2} \\
    & \leq \frac{\displaystyle \sum_{i = 1}^n \left(\int_0^1 |h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*))| dt \right) |x_i - x^*_i|}{\|\bm{x} - \bm{x}^*\|^2} \\
    & = \sum_{i = 1}^n \left(\int_0^1 \frac{|h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*))|}{\|\bm{x} - \bm{x}^*\|} dt \right) \frac{|x_i - x^*_i|}{\|\bm{x} - \bm{x}^*\|} \\
    & \leq \sum_{i = 1}^n \int_0^1 \frac{|h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*))|}{\|\bm{x} - \bm{x}^*\|} dt \\
    & = \sum_{i = 1}^n \int_0^1 |t| \frac{|h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*))|}{\|(\bm{x}^* + t(\bm{x} - \bm{x}^*)) - \bm{x}^*\|} dt \\
    & \leq \sum_{i = 1}^n \int_0^1 \frac{|h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*))|}{\|(\bm{x}^* + t(\bm{x} - \bm{x}^*)) - \bm{x}^*\|} dt \quad \text{(*)}
\end{align*}
$$

である．$h_i$ $(i = 1, \cdots, n)$ は連続であるから，ある $t^*$ $(0 \leq t^* \leq 1)$ が存在して

$$
\begin{equation*}
    \sum_{i = 1}^n \int_0^1 \frac{|h_i(\bm{x}^* + t(\bm{x} - \bm{x}^*))|}{\|(\bm{x}^* + t(\bm{x} - \bm{x}^*)) - \bm{x}^*\|} dt
    = \sum_{i = 1}^n \frac{|h_i(\bm{x}^* + t^*(\bm{x} - \bm{x}^*))|}{\|(\bm{x}^* + t^*(\bm{x} - \bm{x}^*)) - \bm{x}^*\|}
\end{equation*}
$$

である．$\displaystyle \lim_{\bm{x} \to \bm{x}^*} \frac{|h_i(\bm{x})|}{\|\bm{x} - \bm{x}^*\|} = 0$ であり，$\displaystyle \lim_{\bm{x} \to \bm{x}^*} (\bm{x}^* + t^*(\bm{x} - \bm{x}^*)) = \bm{x}^*$ であるから，

$$
\begin{equation*}
    \lim_{\bm{x} \to \bm{x}^*} \sum_{i = 1}^n \frac{|h_i(\bm{x}^* + t^*(\bm{x} - \bm{x}^*))|}{\|(\bm{x}^* + t^*(\bm{x} - \bm{x}^*)) - \bm{x}^*\|} = 0.
\end{equation*}
$$

よって

$$
\begin{equation*}
    \lim_{\bm{x} \to \bm{x}^*} \frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|^2}
\end{equation*}
$$

である ((*) の右辺は広義積分だが，収束するか未確認)．