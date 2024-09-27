## Trọng số của hàm boolean

```{contents}
:depth: 2
```

Ở phần này ký hiệu vector không $\mathbf{0} = (0, \ldots, 0)$, vector một $\mathbf{1} = (1, \ldots, 1)$.

### Trọng số của hàm boolean

````{prf:definition} Trọng số của hàm boolean
**Trọng số** (hay **weight**, **вес**) của hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$ là số lượng giá trị khác $0$ của hàm $f$. 

Ký hiệu là $\mathrm{wt}(f)$.
````

````{prf:example}
Hàm boolean $f(x, y) = (0, 1, 0, 1)$ có trọng số $\mathrm{wt}(f) = 2$.

Hàm boolean $f(x, y, z) = (1, 0, 1, 1, 1, 0, 0, 1)$ có trọng số $\mathrm{wt}(f) = 5$.
````

Một số tính chất của trọng số:

1. $0 \leqslant \mathrm{wt}(f) \leqslant 2^n$
2. $\mathrm{wt}(f \oplus \mathbf{1}) = 2^n - \mathrm{wt}(f)$
3. Nếu $h$ cũng là một hàm boolean từ $\mathbb{F}_2^n$ tới $\mathbb{F}_2$ thì

$$\mathrm{wt}(f \oplus h) = \mathrm{wt}(f) + \mathrm{wt}(h) - 2 \mathrm{wt}(fh)$$

4. Giá trị $\mathrm{wt}(f)$ nhận giá trị lẻ khi và chỉ khi $\deg(f) = n$.

````{prf:definition} Hàm boolean cân bằng
Nếu hàm boolean $n$ biến $f$ có trọng số bằng $2^{n-1}$ thì $f$ được gọi là hàm boolean **cân bằng** (hay **balanced**, **сбалансированная**).
````

````{prf:remark}
1. Ta nói hàm boolean $g$ *giả phụ thuộc* vào biến $y$ nếu $g(x_1, \ldots, x_n, y) = f(x_1, \ldots x_n)$. Khi đó $\mathrm{wt} (g) = 2 \mathrm{wt} (f)$.

2. Đặt $f(x_1, \ldots, x_n)$ và $g(y_1, \ldots, y_m)$ là các hàm boolean phụ thuộc vào tập các biến không giao nhau. Khi đó:

a) nếu $f$ và $g$ là các hàm số khác hằng $1$ thì $f \cdot g$ không là hàm cân bằng;

b) $f$ hoặc $g$ cân bằng khi và chỉ khi $f \oplus g$ cân bằng.
````

```{admonition} **Chứng minh**
:class: danger, dropdown

1. Do 

$$g(x_1, \ldots, x_n, 0) = g(x_1, \ldots, x_n, 1) = f(x_1, \ldots, x_n)$$

nên ta có điều phải chứng minh.

2. Đặt $\mathbf{x} = (x_1, \ldots, x_n)$ và $\mathbf{y} = (y_1, \ldots, y_m)$.

a) Đặt $\mathrm{wt}(f) = r < 2^n$ và $\mathrm{wt}(g) = s < 2^m$. Vì $f(\mathbf{x}) \cdot g(\mathbf{y}) = 1$ khi và chỉ khi $f(\mathbf{x}) = g(\mathbf{y}) = 1$ nên $\mathrm{wt}(f \cdot g) = r \cdot s$. 

Do đó nếu $f \cdot g$ cân bằng thì $2^{n+m-1} = \mathrm{wt}(f \cdot g) = r \cdot s$.

Như vậy $r = 2^k$ và $s = 2^l$ với $k \leqslant n-1$ và $l \leqslant m-1$.

Suy ra $r \cdot s \leqslant 2^{n+m-2}$. Điều này vô lý vì $r \cdot s = 2^{n + m - 1} > 2^{n+m-2}$. Nghĩa là giả sử ban đầu $r < 2^n$ là sai, tương tự với $s$ và ta có điều phải chứng minh.

b) Chú ý rằng $f(\mathbf{x}) \oplus g(\mathbf{y}) = 1$ khi và chỉ khi $f(\mathbf{x}) \neq g(\mathbf{y})$. Suy ra 

$$\mathrm{wt}(f \oplus g) = \mathrm{wt}(f) \cdot \mathrm{wt}(\bar{g}) + \mathrm{wt}(\bar{f}) \cdot \mathrm{wt}(g)$$

*Điều kiện đủ.* Giả sử hàm $f$ cân bằng, suy ra

$$\mathrm{wt}(f) = \mathrm{wt}(\bar{f}) = 2^{n-1}$$

Như vậy

$$\mathrm{wt}(f \oplus g) = 2^{n-1} \cdot \mathrm{wt}(g) + 2^{n-1} \cdot \mathrm{wt}(\bar{g}) = 2^{n-1} \cdot 2^m$$

Vậy $f \oplus g$ là hàm cân bằng.

*Điều kiện cần.* Giả sử $\mathrm{wt}(f) = r \neq 2^{n-1}$ và $\mathrm{wt}(g) = s$. Như vậy

$$\mathrm{wt}(f \oplus g) = r (2^m - s) + s (2^n - r) = 2^{n+m-1}$$

do $f \oplus g$ là hàm cân bằng. Tiếp theo

$$s = \dfrac{2^{n+m-1} - 2^m \cdot r}{2^n - 2r} = 2^{m-1}$$

Vậy $g$ là hàm cân bằng.
```

### Khoảng cách Hamming

````{prf:definition} Khoảng cách Hamming giữa hai vector
Với hai vector $\mathbf{x}$, $\mathbf{y}$ thuộc $\mathbb{F}_2^n$, đặt

$$\begin{equation}
	d (\mathbf{x}, \mathbf{y}) = \mathrm{wt} (\mathbf{x} \oplus \mathbf{y})
\end{equation}$$

là **khoảng cách Hamming** giữa hai vector $\mathbf{x}$ và $\mathbf{y}$. Trong đó $\mathrm{wt}(\mathbf{z})$ là trọng số vector $\mathbf{z}$.
````

````{prf:definition} Khoảng cách Hamming từ vector tới tập vector
Xét $M \subseteq \mathbb{F}_2^n$. Khi đó với mọi $\mathbf{x} \in \mathbb{F}_2^n$, ta nói khoảng cách từ $\mathbf{x}$ tới $M$ là

$$\begin{equation}
	d(\mathbf{x}, M) = \min_{\mathbf{y} \in M} d (\mathbf{x}, \mathbf{y})
\end{equation}$$
````

````{prf:definition} Khoảng cách Hamming giữa hai hàm boolean
Xét hai hàm boolean $n$ biến là $f(x_1, x_2, \ldots, x_n)$ và $g(x_1, x_2, \ldots, x_n)$. Khi đó khoảng cách Hamming từ hàm $f$ tới hàm $g$ là

$$\begin{equation}
	d(f, g) = \mathrm{wt}(f \oplus g) = \sum_{\mathbf{x} \in \mathbb{F}_2^n} f(\mathbf{x}) \oplus g(\mathbf{x})
\end{equation}$$
````
