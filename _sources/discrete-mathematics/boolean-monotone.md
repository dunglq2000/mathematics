## Hàm đơn điệu

````{prf:definition} Vector so sánh được
Xét hai vector $\bm{a} = (a_1, a_2, \ldots, a_n)$ và $\bm{b} = (b_1, b_2, \ldots, b_n)$ ($a_i, b_i \in \{0, 1\}$). Ta nói $\bm{a}$ **so sánh được nhỏ hơn** $\bm{b}$ nếu với mọi $i = 1, 2, \ldots, n$ ta có $a_i \leqslant b_i$. Ký hiệu $\bm{a} \preccurlyeq \bm{b}$.
````

````{prf:example}
Ta có $(1, 0, 0) \preccurlyeq (1, 0, 1)$, còn $(1, 0, 0)$ và $(0, 1, 0)$
thì không so sánh được (vị trí thứ 1 và thứ 2).
````

````{prf:definition} Hàm boolean đơn điệu
Hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$ được gọi là **hàm boolean đơn điệu** (hay **monotone**) nếu với mọi vector $(a_1, a_2, \ldots, a_n) \preccurlyeq (b_1, b_2, \ldots, b_n)$ thì ta có 

$$\begin{equation}
    f(a_1, a_2, \ldots, a_n) \leqslant f(b_1, b_2, \ldots, b_n)  
\end{equation}$$
````

````{prf:example}
Xét hàm boolean $f(x, y) = (0, 1, 0, 1)$.

Ta thấy rằng:
- $(0, 0) \preccurlyeq (0, 1)$ và $f(0, 0) = 0 \leqslant 1 = f(0, 1)$
- $(0, 0) \preccurlyeq (1, 0)$ và $f(0, 0) = 0 \leqslant 0 = f(1, 0)$
- $(0, 0) \preccurlyeq (1, 1)$ và $f(0, 0) = 0 \leqslant 1 = f(1, 1)$
- $(0, 1)$ và $(1, 0)$ không so sánh được nên bỏ qua
- $(0, 1) \preccurlyeq (1, 1)$ và $f(0, 1) = 1 \leqslant 1 = f(1, 1)$
- $(1, 0) \preccurlyeq (1, 1)$ và $f(1, 0) = 0 \leqslant 1 = f(1, 1)$

Vậy đây là hàm đơn điệu.
````