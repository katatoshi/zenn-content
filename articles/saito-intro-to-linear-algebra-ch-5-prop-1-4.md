---
title: "齋藤線型代数入門 第5章 [1.4] ノート"
emoji: "📝"
type: "tech"
topics:
  - "数学"
  - "線形代数"
  - "線型代数"
published: true
---

# はじめに

齋藤『線型代数入門』を読んでいて，第5章 [1.4] の必要性の証明が頭の中できなかった．そのときに書いた証明をここにも残しておく[^1]．

[^1]:https://mathtod.online/@katatoshi/110741625910062325

# 命題と証明

**命題** $\enspace$ 行列 $A$ が対角行列に相似である (すなわち $P^{-1}AP$ が対角行列になるような正則行列 $P$ が存在する) ためには，$A$ の各特性根 $\alpha$ に対する固有空間の次元が，$\alpha$ の重複度に一致することが必要かつ十分な条件である．

**証明** $\enspace$ (十分性) $\alpha_1, \cdots, \alpha_k$ を $A$ のすべての特性根とし，$\alpha_i$ の重複度を $n_i$ とする．$A$ の次数を $n$ とすると $n_1 + \cdots + n_k = n$ である．$\alpha_i$ に対する固有空間 $W_i$ の次元が $\alpha_i$ の重複度に一致するならば $\dim(W_1) + \cdots + \dim(W_k)$ $= \dim(\bm{C}^n)$ となるので，$W_1 \dotplus \cdots \dotplus W_k$ $= \bm{C}^n$ が成り立つ．よって [1.2] より $A$ は対角行列に相似である．

(必要性) $\alpha_1, \cdots, \alpha_k$ を $A$ のすべての固有値とし，$\alpha_i$ に対する固有空間を $W_i$ とする．$A$ が対角行列に相似であるとすると，[1.2] より $W_1 \dotplus \cdots \dotplus W_k$ $= \bm{C}^n$ が成り立つ．$W_i$ の次元を $n_i$ とし，$W_i$ の基底を $E_i = \langle \bm{e}_{m_i + 1}, \cdots, \bm{e}_{m_i + n_i} \rangle$ ($m_i = \sum_{j < i} n_j$) とすると，$E = \langle \bm{e}_1, \cdots, \bm{e}_n \rangle$ は $\bm{C}^n$ の基底となる．$E_i$ に関する $T_A\vert_{W_i}$ [^2]の行列を $B_i$，$E$ に関する $T_A$ の行列を $B$ とすると，各 $W_i$ は $T_A$ による不変部分空間なので，

[^2]:$T_A\vert_{W_i}$ は写像 $T_A: \bm{C}^n \to \bm{C}^n$ の $W_i$ への制限．

$$
\begin{equation*}
B =
  \begin{pmatrix}
    B_1 &        & O \\
        & \ddots & \\
    O   &        & B_k
  \end{pmatrix}
\end{equation*}
$$

となる (p.119)．$T_A\vert_{W_i} = T_{A_i}$ とすると，正則行列 $P_i$ が存在して $B_i = P_i^{-1}A_iP_i$ と書けるが，$T_A\vert_{W_i}$ はスカラー変換 $\alpha_i \operatorname{id}_{W_i}$ [^3]であるから $A_i = \alpha_i I_{n_i}$ [^4]となり，$B_i = \alpha_i I_{n_i}$ であることがわかる．$B$ は正則行列 $P$ が存在して $B = P^{-1}AP$ と書けるので，

[^3]:$\operatorname{id}_X$ は集合 $X$ 上の恒等変換．
[^4]:$I_l$ は $l$ 次単位行列．

$$
\begin{equation*}
P^{-1}AP =
  \begin{pmatrix}
    \alpha_1 I_{n_1} &        & O \\
                     & \ddots & \\
    O                &        & \alpha_k I_{n_k}
  \end{pmatrix}
\end{equation*}
$$

が成り立つ．よって，$A$ の特性多項式は

$$
\begin{align*}
\Phi_A(x) &= \Phi_{P^{-1}AP}(x) \\
          &= \det(xI_n - P^{-1}AP) \\
          &=
  \begin{vmatrix}
    (x - \alpha_1) I_{n_1} &        & O \\
                           & \ddots & \\
    O                      &        & (x - \alpha_k) I_{n_k}
  \end{vmatrix} \\
          &= (x - \alpha_1)^{n_1} \cdots (x - \alpha_k)^{n_k}
\end{align*}
$$

となるので，特性根 $\alpha_i$ の重複度は $\alpha_i$ に対する固有空間の次元に一致する．$\enspace$ (証明終)

# 参考文献

* 齋藤正彦『線型代数入門』東京大学出版会，1966．
