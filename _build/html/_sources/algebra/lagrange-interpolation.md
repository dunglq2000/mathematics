## Đa thức nội suy Lagrange

Trong đại số, công thức nội suy Lagrange cho phép chúng ta tìm được một đa thức $f(x)$ trên trường $\mathbb{F}$ bất kì khi biết được một số cặp $(x_i, f(x_i))$ nhất định ($x_i, f(x_i) \in \mathbb{F}$).

Để tìm đa thức $f(x)$ có bậc $n$ ta cần ít nhất $n+1$ cặp $(x_i, f(x_i) = y_i)$, với $1 \leqslant i \leqslant n+1$ và $x_i \neq x_j$ với mọi $i \neq j$.

Khi đó, ta có \textbf{công thức nội suy Lagrange} như sau:

$$\begin{equation*}
    \displaystyle{f(x) = \sum_{i=1}^{n+1} \left(y_i \cdot \prod_{j \neq i} \frac{x - x_j}{x_i - x_j}\right)}
\end{equation*}$$

````{prf:example}
Giả sử chúng ta có hàm $f(x) = x^2 + x + 1$. Khi đó $f(1) = 3, f(-1) = 1, f(0) = 1$.

Từ ba cặp $(x_i, f(x_i))$ trên mình sẽ tìm ngược lại $f(x)$ ban đầu.

Theo công thức thì

$$\begin{align*}
    f(x) = & y_1 \cdot \frac{(x - x_2) (x - x_3)}{(x_1 - x_2) (x_1 - x_3)} + y_2 \cdot \frac{(x - x1) (x - x_3)}{(x_2 - x_1) (x_2 - x_3)} \\
    + & y_3 \cdot \frac{(x - x1) (x - x_2)}{(x_3 - x1) (x_3 - x_2)}
\end{align*}$$

Thay số vào thì ta có

$$\begin{equation*}
    \displaystyle{f(x) = 3 \cdot \frac{(x - (-1)) (x - 0)}{(1 - (-1)) (1 - 0)} + 1 \cdot \frac{(x - 1) (x - 0)}{(-1 - 1) (-1 - 0)} + 1 \cdot \frac{(x - 1) (x - (-1))}{(0 - 1) (0 - (-1))}}
\end{equation*}$$

Thu gọn lại ta có $f(x) = x^2 + x + 1$ (đúng với hàm cần tìm).
````