---
title: "1点で2回微分可能なら2次近似できることの証明"
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

と書いてあって，1点で2回微分可能ってだけで2次近似できるんだっけ？　と気になったので証明してみた[^1]．

[^1]:笠原『微分積分学』，杉浦『解析入門』，小平『解析入門』，黒田『微分積分』をざっと調べた限り，この命題は載ってなさそうだった．笠原にはヘッセ行列は載っていたが，2次近似については載っていなかった．杉浦，小平に関してはヘッセ行列すら載っていなかった．黒田にはヘッセ行列と2次近似についても載っていたが，$C^3$-級を仮定している (テイラーの公式)．

# 微分可能性と記号の定義

以下，微分可能性の定義は笠原『微分積分学』を参考にした．勾配ベクトル，ヘッセ行列の記法は矢部を参考にした．

$D$ を $\bm{R}^n$ の領域 (連結な開集合) とし，$f: D \to \bm{R}$ とする．$f$ が $\bm{x}^* \in D$ で (1回) 微分可能であるとは，あるベクトル $\bm{a} \in \bm{R}$ が存在して

$$
\begin{align*}
    & f(\bm{x}) = f(\bm{x}^*) + \bm{a}^\mathrm{T} (\bm{x} - \bm{x}^*) + g(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|} = 0
\end{align*}
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

である．ベクトル

$$
\nabla f(\bm{x}) =
\begin{pmatrix}
    {\displaystyle \frac{\partial f}{\partial x_1}(\bm{x})} \\
    \vdots \\
    {\displaystyle \frac{\partial f}{\partial x_n}(\bm{x})} \\
\end{pmatrix}
$$

を $f$ の勾配ベクトルと呼ぶ．勾配ベクトルの記号を用いれば $f$ が $\bm{x}^*$ で微分可能であることは

$$
\begin{align*}
    & f(\bm{x}) = f(\bm{x}^*) + \nabla f(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*) + g(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|} = 0
\end{align*}
$$

と書ける．

領域 $D$ の各点で微分可能な関数 $f: D \to \bm{R}$ が $\bm{x}^* \in D$ で2回微分可能であるとは，$f$ のすべての偏導関数 $\frac{\partial f}{\partial x_i}$ $(i = 1, \cdots, n)$ が $\bm{x}^*$ で微分可能，すなわち，すべての $i = 1, \cdots, n$ について

$$
\begin{align*}
    & \frac{\partial f}{\partial x_i}(\bm{x}) = \frac{\partial f}{\partial x_i}(\bm{x}^*) + \nabla \frac{\partial f}{\partial x_i}(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*) + g_i(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{g_i(\bm{x})}{\|\bm{x} - \bm{x}^*\|} = 0
\end{align*}
$$

が成り立つことである．行列

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

を $f$ のヘッセ行列と呼ぶ[^2]．2回微分可能の条件をベクトルにまとめると

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

となるので，$\bm{g}(\bm{x}) = (g_1(\bm{x}), \cdots, g_n(\bm{x}))^\mathrm{T}$ として，勾配ベクトルとヘッセ行列を用いれば $f$ が $\bm{x}^*$ で2回微分可能であることは

$$
\begin{align*}
    & \nabla f(\bm{x}) = \nabla f(\bm{x}^*) + \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) + \bm{g}(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{\bm{g}(\bm{x})}{\|\bm{x} - \bm{x}^*\|} = \bm{0}
\end{align*}
$$

と書ける．

# 1変数の場合

1変数の場合はロピタルの定理が使えるので簡単に証明できる．

**命題** $\enspace$ 区間 $D = (a, b)$ $(a < x^* < b)$ で定義された関数 $f$ が $D$ 上微分可能で，$x^*$ で2回微分可能であるとする．このとき

$$
\begin{align*}
    & f(x) = f(x^*) + f^\prime(x^*) (x - x^*) + \frac{1}{2} f^{\prime\prime}(x^*) (x - x^*)^2 + g(x), \\
    & \lim_{x \to x^*} \frac{g(x)}{(x - x^*)^2} = 0.
\end{align*}
$$

**証明** $\enspace$

$$
g(x) = f(x) - f(x^*) - f^\prime(x^*) (x - x^*) - \frac{1}{2} f^{\prime\prime}(x^*) (x - x^*)^2
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
\lim_{x \to x^*} \frac{g(x)}{(x - x^*)^2} = \lim_{x \to x^*} \frac{g^\prime(x)}{((x - x^*)^2)^\prime} = 0
$$

が成り立つ. $\enspace$ (証明終)

# 多変数の場合

多変数の場合はロピタルの定理が使えないので証明がちょっと面倒になる．証明には次の多変数関数の平均値の定理を使う．

**定理** (平均値の定理)[^3] $\enspace$ $f$ は領域 $D$ 上で定義されているとし，$\bm{x}^*$, $\bm{x}$ およびこの2点を結ぶ線分が $D$ に属するものとする．$f$ が $D$ で微分可能なら，

$$
f(\bm{x}) - f(\bm{x}^*) = \nabla f(\bm{x}^* + \theta(\bm{x} - \bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*)
$$

をみたす $\theta$ $(0 < \theta < 1)$ が存在する．

[^3]:笠原 定理 5.16.

**命題** $\enspace$ 領域 $D$ で定義された関数 $f$ が $D$ 上微分可能で，$x^* \in D$ で2回微分可能であるとする．このとき

$$
\begin{align*}
    & f(\bm{x}) = f(\bm{x}^*) + \nabla f(\bm{x}^*)^\mathrm{T}(\bm{x} - \bm{x}^*) + \frac{1}{2} (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) + g(\bm{x}), \\
    & \lim_{\bm{x} \to \bm{x}^*} \frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|^2} = 0.
\end{align*}
$$

**証明** $\enspace$

$$
g(\bm{x}) = f(\bm{x}) - f(\bm{x}^*) - \nabla f(\bm{x}^*)^\mathrm{T}(\bm{x} - \bm{x}^*) - \frac{1}{2} (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*)
$$

とすると，$g$ は $D$ で微分可能である．$D$ は開集合なので $U_\varepsilon(\bm{x}^*) \subset D$ となる $\varepsilon > 0$ が存在する[^4]．そのような $\varepsilon$ を1つ選び $U = U_\varepsilon(\bm{x}^*)$ とする．$\bm{x} \in U$ とすると，$\bm{x}^*$, $\bm{x}$ およびこの2点を結ぶ線分は $U$ に属するので，平均値の定理より

[^4]:$U_\varepsilon(\bm{x}^*) = \{\bm{x} \mid \|\bm{x} - \bm{x}^*\| < \varepsilon \}$.

$$
\begin{align*}
    & g(\bm{x}) \\
    & = g(\bm{x}^*) + \nabla g(\bm{x}^* + \theta(\bm{x} - \bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \nabla g(\bm{x}^* + \theta(\bm{x} - \bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \left(\nabla f(\bm{x}^* + \theta(\bm{x} - \bm{x}^*)) - \nabla f(\bm{x}^*) - \frac{\theta}{2} (\nabla^2 f(\bm{x}^*) + \nabla^2 f(\bm{x}^*)^\mathrm{T}) (\bm{x} - \bm{x}^*)\right)^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = (\nabla f(\bm{x}^* + \theta(\bm{x} - \bm{x}^*)) - \nabla f(\bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & \qquad - \frac{\theta}{2} \left(\left(\nabla^2 f(\bm{x}^*) + \nabla^2 f(\bm{x}^*)^\mathrm{T}\right) (\bm{x} - \bm{x}^*)\right)^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = (\nabla f(\bm{x}^* + \theta(\bm{x} - \bm{x}^*)) - \nabla f(\bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & \qquad - \frac{\theta}{2} (\bm{x} - \bm{x}^*)^\mathrm{T} \left(\nabla^2 f(\bm{x}^*) + \nabla^2 f(\bm{x}^*)^\mathrm{T}\right)^\mathrm{T} (\bm{x} - \bm{x}^*)
\end{align*}
$$

をみたす $\theta$ $(0 < \theta < 1)$ が存在する．$f$ は $\bm{x}^*$ で2回微分可能だから $\nabla^2 f(\bm{x}^*)$ は対称行列となるので[^5]

[^5]:$f$ が $\bm{x}^*$ で2回微分可能なら $\frac{\partial^2 f}{\partial x_j \partial x_i} = \frac{\partial^2 f}{\partial x_i \partial x_j}$ $(i, j = 1, \cdots, n)$ が成り立つ．笠原 定理5.10.

$$
g(\bm{x}) = (\nabla f(\bm{x}^* + \theta(\bm{x} - \bm{x}^*)) - \nabla f(\bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) - \theta (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*)
$$

である．$\bm{x}$ ごとにこの式が成り立つような $\theta$ が存在するので，各 $\bm{x} \in U$ に対して，この式が成り立つような $\theta$ を1つ選び $\theta(\bm{x})$ とする．この式の右辺の各項を成分で表すと

$$
\begin{align*}
    & (\nabla f(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \nabla f(\bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) \\
    & = \sum_{i = 1}^n \left(\frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*)\right) (x_i - x^*_i),
\end{align*}
$$

$$
\begin{align*}
    & \theta(\bm{x}) (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*) \\
    & = \sum_{i = 1}^n \left(\sum_{j = 1}^n \frac{\partial^2 f}{\partial x_j \partial x_i}(\bm{x}^*) \theta(\bm{x}) (x_j - x^*_j)\right) (x_i - x^*_i)
\end{align*}
$$

となるので

$$
\begin{align*}
    & \left|\frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|^2}\right| \\
    & = \left|\frac{\displaystyle (\nabla f(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \nabla f(\bm{x}^*))^\mathrm{T} (\bm{x} - \bm{x}^*) - \theta(\bm{x}) (\bm{x} - \bm{x}^*)^\mathrm{T} \nabla^2 f(\bm{x}^*) (\bm{x} - \bm{x}^*)}{\|\bm{x} - \bm{x}^*\|^2}\right| \\
    & = \left|\sum_{i = 1}^n \frac{\displaystyle \left(\frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \sum_{j = 1}^n \frac{\partial^2 f}{\partial x_j \partial x_i}(\bm{x}^*) \theta(\bm{x}) (x_j - x^*_j)\right) (x_i - x^*_i)}{\|\bm{x} - \bm{x}^*\|^2}\right| \\
    & = \left|\sum_{i = 1}^n \frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \sum_{j = 1}^n \frac{\partial^2 f}{\partial x_j \partial x_i}(\bm{x}^*) \theta(\bm{x}) (x_j - x^*_j)}{\|\bm{x} - \bm{x}^*\|} \frac{x_i - x^*_i}{\|\bm{x} - \bm{x}^*\|}\right| \\
    & \leq \sum_{i = 1}^n \left|\frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \sum_{j = 1}^n \frac{\partial^2 f}{\partial x_j \partial x_i}(\bm{x}^*) \theta(\bm{x}) (x_j - x^*_j)}{\|\bm{x} - \bm{x}^*\|}\right| \left|\frac{x_i - x^*_i}{\|\bm{x} - \bm{x}^*\|}\right| \\
    & \leq \sum_{i = 1}^n \left|\frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \sum_{j = 1}^n \frac{\partial^2 f}{\partial x_j \partial x_i}(\bm{x}^*) \theta(\bm{x}) (x_j - x^*_j)}{\|\bm{x} - \bm{x}^*\|}\right| \\
    & = \sum_{i = 1}^n \left|\frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \nabla \frac{\partial f}{\partial x_i}(\bm{x}^*)^\mathrm{T} (\theta(\bm{x}) (\bm{x} - \bm{x}^*))}{\|\bm{x} - \bm{x}^*\|}\right| \\
    & = \sum_{i = 1}^n \theta(\bm{x}) \left|\frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \nabla \frac{\partial f}{\partial x_i}(\bm{x}^*)^\mathrm{T} (\theta(\bm{x}) (\bm{x} - \bm{x}^*))}{\|\theta(\bm{x})(\bm{x} - \bm{x}^*)\|}\right| \\
    & \leq \sum_{i = 1}^n \left|\frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \nabla \frac{\partial f}{\partial x_i}(\bm{x}^*)^\mathrm{T} (\theta(\bm{x}) (\bm{x} - \bm{x}^*))}{\|\theta(\bm{x})(\bm{x} - \bm{x}^*)\|}\right| \\
    & = \sum_{i = 1}^n \left|\frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \nabla \frac{\partial f}{\partial x_i}(\bm{x}^*)^\mathrm{T} ((\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \bm{x}^*)}{\|(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) - \bm{x}^*\|}\right|
\end{align*}
$$

が成り立つ．$f$ は $\bm{x}^*$ で2回微分可能であるから

$$
\begin{equation*}
    \lim_{\bm{x} \to \bm{x}^*} \frac{\displaystyle \frac{\partial f}{\partial x_i}(\bm{x}) - \frac{\partial f}{\partial x_i}(\bm{x}^*) - \nabla \frac{\partial f}{\partial x_i}(\bm{x}^*)^\mathrm{T} (\bm{x} - \bm{x}^*)}{\|\bm{x} - \bm{x}^*\|} = 0
\end{equation*}
$$

であり，$\bm{x} \to \bm{x}^*$ のとき $(\bm{x}^* + \theta(\bm{x})(\bm{x} - \bm{x}^*)) \to \bm{x}^*$ であるから，上の不等式の最右辺は $\bm{x} \to \bm{x}^*$ のとき $0$ に収束する．よって

$$
\begin{equation*}
    \lim_{\bm{x} \to \bm{x}^*} \frac{g(\bm{x})}{\|\bm{x} - \bm{x}^*\|^2} = 0
\end{equation*}
$$

である．$\enspace$ (証明終)

# 参考文献

* 笠原晧司『微分積分学』サイエンス社，1974．
* 黒田成俊『微分積分』共立出版，2002．
* 小平邦彦『軽装版 解析入門 I』岩波書店，2003．
* 小平邦彦『軽装版 解析入門 II』岩波書店，2003．
* 杉浦光夫『解析入門1』東京大学出版会，1980．
* 杉浦光夫『解析入門2』東京大学出版会，1985．
* 矢部博『工学基礎 最適化とその応用』数理工学社，2006．