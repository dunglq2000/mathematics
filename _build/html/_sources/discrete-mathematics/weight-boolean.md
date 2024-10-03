## Khoảng cách Hamming

````{prf:definition} Khoảng cách Hamming giữa hai vector
Với hai vector $\bm{x}$, $\bm{y}$ thuộc $\mathbb{F}_2^n$, đặt

$$\begin{equation}
	d (\bm{x}, \bm{y}) = \mathrm{wt} (\bm{x} \oplus \bm{y})
\end{equation}$$

là **khoảng cách Hamming** giữa hai vector $\bm{x}$ và $\bm{y}$. Trong đó $\mathrm{wt}(\bm{z})$ là trọng số vector $\bm{z}$.
````

````{prf:definition} Khoảng cách Hamming từ vector tới tập vector
Xét $M \subseteq \mathbb{F}_2^n$. Khi đó với mọi $\bm{x} \in \mathbb{F}_2^n$, ta nói khoảng cách từ $\bm{x}$ tới $M$ là

$$\begin{equation}
	d(\bm{x}, M) = \min_{\bm{y} \in M} d (\bm{x}, \bm{y})
\end{equation}$$
````

````{prf:definition} Khoảng cách Hamming giữa hai hàm boolean
Xét hai hàm boolean $n$ biến là $f(x_1, x_2, \ldots, x_n)$ và $g(x_1, x_2, \ldots, x_n)$. Khi đó khoảng cách Hamming từ hàm $f$ tới hàm $g$ là

$$\begin{equation}
	d(f, g) = \mathrm{wt}(f \oplus g) = \sum_{\bm{x} \in \mathbb{F}_2^n} f(\bm{x}) \oplus g(\bm{x})
\end{equation}$$
````
