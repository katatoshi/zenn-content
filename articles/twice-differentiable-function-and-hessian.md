---
title: "2回微分可能な多変数関数とヘッセ行列についてのノート"
emoji: "📝"
type: "tech"
topics:
  - "数学"
  - "最適化"
  - "微積分"
published: false
---

# はじめに

矢部『工学基礎　最適化とその応用』で
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

と書いてあって，まあ成り立つかな...2回微分可能なだけで成り立つんだっけ，これ？　となったので確認した際のノートを整理して書き留めておく．

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

を $f$ のヘッセ行列と呼ぶ[^1]．$(4)$ をベクトルにまとめると

[^1]:$\frac{\partial^2 f}{\partial x_j \partial x_i} = \frac{\partial}{\partial x_j}\left(\frac{\partial f}{\partial x_i}\right)$．

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

$f$ が $\bm{x}^*$ で2回微分可能なら，$f$ のすべての偏導関数 $\frac{\partial f}{\partial x_i}$ $(i = 1, \cdots, n)$ が $\bm{x}^*$ で連続なので，$f$ は...$C^1$-級と言いたかったけど，$\bm{x}^*$ 以外の点の連続性については何も言えていないので，$D$ 上で $C^1$-級とは言えない...．

# 件の命題が成り立つことの確認

**定理** (積分公式)[^2] $f(\bm{x})$ が領域 $D$ 上で $C^1$-級なら，



[^2]:笠原 定理 5.17