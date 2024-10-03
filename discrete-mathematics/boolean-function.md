## Hàm boolean

```{contents}
```

### Algebraic Normal Form

Đặt $f(\bm{x})$ là hàm boolean $n$ biến. Với số $m \leqslant n$ thì

$$\begin{align*}
  f(x_1, \ldots, x_n) = \bigoplus_{a_1, \ldots, a_m \in \mathbb{F}_2} & (x_1 \oplus a_1 \oplus 1) \times \cdots \times \\
  \times & (x_m \oplus a_m \oplus 1) \cdot f(a_1, \ldots, a_m, x_{m+1}, \ldots, x_n)
\end{align*}$$

```{admonition} **Chứng minh**
:class: danger, dropdown

Chọn bộ $(b_1, \ldots, b_m)$ bất kì thuộc $\mathbb{F}_2^m$.

Thay $x_i$ bởi $b_i$ với $i = 1, \ldots, m$ thì

$$\begin{align*}
  f(b_1, \ldots, b_m, x_{m+1}, x_m) = \bigoplus_{a_1, \ldots, a_m \in \mathbb{F}_2} (b_1 \oplus a_1 \oplus 1) \cdots (b_m \oplus a_m \oplus 1) \cdot f(a_1, \ldots, a_m, x_{m+1}, \ldots, x_n)
\end{align*}$$

Ở vế phải, tích $\prod\limits_{i=1}^m (b_i \oplus a_i \oplus 1) = 1$ khi và chỉ khi $b_i \oplus a_i \oplus 1 = 1$ với mọi $i = 1, \ldots, m$. 

Nói cách khác là khi $b_i \equiv a_i$ thì ta còn $f$ ở vế phải, còn các trường hợp kia thì bằng $0$. Do đó ta có điều phải chứng minh.
```

Khi đó, $f(a_1, \ldots, a_m, x_{m+1}, \ldots, x_m)$ được gọi là **hệ số khai triển của hàm $f$ theo các biến $x_1$, ..., $x_m$**.

````{prf:example}
Xét $f(x_1, x_2) = x_1 x_2 \oplus 1$. Với $m = 1$, ta có

$$\begin{align*}
  a_1 = 0 & \Rightarrow (x_1 \oplus 0 \oplus 1) \cdot f(0, x_2) = (x_1 \oplus 1) \cdot 1 = x_1 \oplus 1 \\
  a_1 = 1 & \Rightarrow (x_1 \oplus 1 \oplus 1) \cdot f(1, x_2) = x_1 \oplus (x_2 \oplus 1)
\end{align*}$$

Như vậy

$$f(x_1, x_2) = (x_1 \oplus 1) \oplus \left(x_1 \cdot (x_2 \oplus 1)\right)$$

Nếu khai triển vế phải ra chúng ta thấy bằng với hàm $f$ ban đầu.
````

Tương ứng với $m$ biến ta có $2^m$ hệ số khai triển.

Đặt $f_1, \ldots, f_{2^m}$ là các hệ số khai triển hàm $f$ theo $m$ biến bất kì. Khi đó

$$\mathrm{wt}(f) = \sum_{i=1}^{2^m} \mathrm{wt} (f_i)$$ (wt-decomp)

````{prf:definition} Algebraic Normal Form
Với hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$, **algrebaric normal form** (hay **ANF**, **dạng chuẩn tắc đại số**, **алгебраическая нормальная форма**) tương ứng với hàm bool đó là cách biểu diễn đa thức đó dưới dạng tổng các tích như sau

$$\begin{equation}
    f(x_1, x_2, \ldots, x_n) = a_0 \oplus a_1 x_1 
    \oplus a_2 x_2 \oplus a_3 x_1 x_2 \oplus \ldots 
    \oplus a_k x_1 x_2 \ldots x_n
\end{equation}$$

với $a_i \in \{0, 1\}$. Ta thấy rằng có $n$ biến, do đó có $2^n$ hệ số $a_i$ ($i = 0, 1, \ldots, 2^n-1$).
````

Trong các tài liệu tiếng Nga thì ANF còn được gọi là **đa thức Zhegalkin** (hay **полином Жегалкина**)

````{prf:definition} Bậc của đa thức Zhegalkin
Tương tự như bậc của một đa thức đại số thông thường, bậc của đa thức Zhegalkin là bậc của hạng tử chứa nhiều đơn thức $x_i$ nhất. Ký hiệu là $\deg(f)$.
````

````{prf:example}
Xét hàm boolean $f(x, y, z) = 1 \oplus x \oplus yz \oplus xyz$. Khi đó $\deg(f) = 3$ vì hạng tử chứa nhiều đơn thức nhất là $xyz$ có 3 đơn thức.

Xét hàm boolean $f(x, y, z) = 1 \oplus z \oplus zy \oplus xy$. Khi đó $\deg(f) = 2$ vì hạng tử chứa nhiều đơn thức nhất là $zy$ (cũng có thể xét $xy$).
````

````{prf:definition} Trọng số của hàm boolean
**Trọng số** (hay **weight**, **вес**) của hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$ là số lượng giá trị khác $0$ của hàm $f$. 

Ký hiệu là $\mathrm{wt}(f)$.
````

````{prf:example}
Hàm boolean $f(x, y) = (0, 1, 0, 1)$ có trọng số $\mathrm{wt}(f) = 2$.

Hàm boolean $f(x, y, z) = (1, 0, 1, 1, 1, 0, 0, 1)$ có trọng số $\mathrm{wt}(f) = 5$.
````

````{prf:property} Một số tính chất của trọng số

Gọi $f$ là hàm boolean $n$ biến. Khi đó:

1. $0 \leqslant \mathrm{wt}(f) \leqslant 2^n$
2. $\mathrm{wt}(f \oplus \bm{1}) = 2^n - \mathrm{wt}(f)$
3. Nếu $h$ cũng là một hàm boolean $n$ biến thì

$$\mathrm{wt}(f \oplus h) = \mathrm{wt}(f) + \mathrm{wt}(h) - 2 \mathrm{wt}(fh)$$

4. $\mathrm{wt}(f)$ nhận giá trị lẻ khi và chỉ khi $\deg(f) = n$.
````

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

2. Đặt $\bm{x} = (x_1, \ldots, x_n)$ và $\bm{y} = (y_1, \ldots, y_m)$.

a) Đặt $\mathrm{wt}(f) = r < 2^n$ và $\mathrm{wt}(g) = s < 2^m$. Vì $f(\bm{x}) \cdot g(\bm{y}) = 1$ khi và chỉ khi $f(\bm{x}) = g(\bm{y}) = 1$ nên $\mathrm{wt}(f \cdot g) = r \cdot s$. 

Do đó nếu $f \cdot g$ cân bằng thì $2^{n+m-1} = \mathrm{wt}(f \cdot g) = r \cdot s$.

Như vậy $r = 2^k$ và $s = 2^l$ với $k \leqslant n-1$ và $l \leqslant m-1$.

Suy ra $r \cdot s \leqslant 2^{n+m-2}$. Điều này vô lý vì $r \cdot s = 2^{n + m - 1} > 2^{n+m-2}$. Nghĩa là giả sử ban đầu $r < 2^n$ là sai, tương tự với $s$ và ta có điều phải chứng minh.

b) Chú ý rằng $f(\bm{x}) \oplus g(\bm{y}) = 1$ khi và chỉ khi $f(\bm{x}) \neq g(\bm{y})$. Suy ra 

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

Đặt

$$
  f(x_1, \ldots, x_n) = \bigoplus_{a_1, \ldots, a_n \in \mathbb{F}_2} g(a_1, \ldots, a_n) \cdot x_1^{a_1} \cdots x_n^{a_n}
$$ (g)

Hàm $g$ khi đó được gọi là **hệ số ANF** của hàm $f$.

Ánh xạ $\mu(f) = g$ được gọi là **biến đổi Mobius** (hay **преобразование Мёбиуса**).

````{prf:example}
Cho hàm bool $f(x, y) = x \vee y$. Ta có bảng chân trị sau

| $x$ | $y$ | $f(x, y)$ |
| --- | --- | --------- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Bảng chân trị này tương đương với đa thức Zhegalkin

$$f(x, y) = x \oplus y \oplus xy$$

````

ANF ở ví dụ trên có thể được viết lại

$$f(x, y) = 0 \cdot x^0 y^0 \oplus 1 \cdot x^0 y^1 \oplus 1 \cdot x^1 y^0 \oplus 1 \cdot x^1 y^1$$

Như vậy biến đổi Mobius của hàm $f$ là

| $x$ | $y$ | $f(x, y)$ | $g = \mu(f)$ |
| --- | --- | --------- | ------------ |
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 |

Ta ký hiệu $\bm{x}^{\bm{a}} = x_1^{a_1} \cdots x_n^{a_n}$ với

- $\bm{x} = (x_1, \ldots, x_n)$
- $\bm{a} = (a_1, \ldots, a_n)$

Do $x_i^{a_i} = 1$ khi và chỉ khi $a_i \leqslant x_i$, ta có $\bm{x}^{\bm{a}} = 1$ khi và chỉ khi $\bm{a} \preccurlyeq \bm{x}$ theo nghĩa $a_i \leqslant x_i$ với $i = 1, \ldots, n$.

Ta có thể viết lại {eq}`g` là

$$f(\bm{x}) = \bigoplus_{\bm{a} \in \mathbb{F}_2^n} g(\bm{a}) \cdot \bm{x}^{\bm{a}} = \bigoplus_{\bm{a} \in \mathbb{F}_2^n} g(\bm{a})$$

````{prf:remark} Biến đổi Mobius
Đặt $f \in \mathcal{F}_n$ và $g = \mu(f)$. Khi đó với mọi $\bm{a} \in \mathbb{F}_2^n$ ta có

$$g(\bm{a}) = \bigoplus_{\bm{x} \preccurlyeq \bm{a}} f(\bm{x})$$
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Ta chứng minh bằng quy nạp theo trọng số của $\bm{a}$.

Ở bước cơ sở khi trọng số bằng không, $g(\bm{0}) = f(\bm{0})$ với $\bm{0}$ là vector chứa $n$ số $0$.

Giả thiết quy nạp: giả sử mệnh đề đúng với mọi vector $\bm{a}$ có trọng số nhỏ hơn $p$.

Khi $\bm{a}$ có trọng số bằng $p$, ta có

$$\begin{align*}
  f(\bm{a}) = \bigoplus_{\bm{x} \preccurlyeq \bm{a}} g(\bm{x}) & = \left( \bigoplus_{\bm{x} \prec \bm{a}} g(\bm{x}) \right) \oplus g(\bm{a}) \quad (\text{tách thành phần nhỏ hơn và bằng} \, \bm{a}) \\
  & = \left(\bigoplus_{\bm{x} \prec \bm{a}} \bigoplus_{\bm{y} \preccurlyeq \bm{x}} f(\bm{y})\right) \oplus g(\bm{a}) \quad (\text{sử dụng giả thiết quy nạp thay} \, g(\bm{x}))
\end{align*}$$

Đặt 

$$S = \bigoplus_{\bm{x} \prec \bm{a}} \bigoplus_{\bm{y} \preccurlyeq \bm{x}} f(\bm{y}) = \bigoplus_{\bm{y} \prec \bm{a}} f(\bm{y}) \bigoplus_{\bm{y} \preccurlyeq \bm{x} \prec \bm{a}} 1 = \bigoplus_{\bm{y} \prec \bm{a}} f(\bm{y})$$

Đẳng thức thứ hai đúng là do $\bm{y}$ nhận tất cả vector từ $\bm{0}$ tới $\bm{x}$ mà $\bm{x} \prec \bm{a}$ nên thực chất có thể thay $\bm{x}$ thành $\bm{y}$.

Đẳng thức cuối đúng là do $2^{\mathrm{wt}(\bm{a}) - \mathrm{wt}(\bm{y})} - 1$ là số lẻ nào đó mà $\bm{y} \preccurlyeq \bm{x} \prec \bm{a}$. Suy ra $g(\bm{a}) = S \oplus f(\bm{a}) = \bigoplus\limits_{\bm{y} \preccurlyeq \bm{a}} f(\bm{y})$.
```

````{prf:corollary}
$$\mu(\mu(f)) = f$$
````

````{prf:remark}
$$g(\bm{1}) = \bigoplus_{\bm{x} \in \mathbb{F}_2^n} f(\bm{x})$$

với $\bm{1}$ là vector có $n$ số $1$.
````

````{prf:remark}
Nếu $f \in \mathcal{F}_n$ và $\deg f = d \geqslant 1$ thì

$$2^{n - d} \leqslant \mathrm{wt} (f) \leqslant 2^n - 2^{n-d}$$
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Đặt $x_{i_1} \cdots x_{i_d}$ là đơn thức có bậc cao nhất ở ANF. Khai triển $f$ thành $n-d$ biến và đặt $f_1, \ldots, f_{2^{n-d}}$ là các hệ số khai triển.

Ở ANF, mỗi hệ số đều có $x_{i_1}$, ..., $x_{i_d}$ nên mọi hệ số đều khác hằng. Suy ra

$$1 \leqslant \mathrm{wt} (f_i) \leqslant 2^d - 1$$

với $i = 1, \ldots, 2^{n-d}$. Ta có điều phải chứng minh.
```

Nói riêng, nếu $\deg f = 1$ thì $f$ là hàm cân bằng.

### Phụ thuộc tuyến tính

````{prf:definition}
Hàm $f(x_1, \ldots, x_n)$ được gọi là **linear dependent** (hay **линейно зависить**) vào biến $x_i$ nếu $f$ có thể biểu diễn ở dạng

$$f(x_1, \ldots, x_n) = g(x_1, \ldots, x_{i-1}, x_{i+1}, \ldots, x_n) \oplus x_i$$

với $g \in \mathcal{F}_{n-1}$.
````

Theo trường hợp riêng ở trên thì nếu $f$ linear dependent vào một biến bất kì thì $f$ là hàm cân bằng.

Ta có thể diễn đạt định nghĩa trên theo cách khác:

$$f(x_1, \ldots, x_{i-1}, 0, x_{i+1}, \ldots, x_n) \neq f(x_1, \ldots, x_{i-1}, 1, x_{i+1}, \ldots, x_n)$$

````{prf:definition}
Hàm $f(x_1, \ldots, x_n)$ được gọi là **quasi-linear dependent** (hay **квазилинейно зависить**) trên cặp biến $x_i$ và $x_j$ nếu $f$ đổi giá trị khi ta đảo giá trị ở vị trí $i$ và $j$.

Nói cách khác, ta có

$$\begin{align*}
  f(x_1, \ldots, x_i, \ldots, x_j, \ldots, x_n) = \bar{f}(x_1, \ldots, \bar{x}_i, \ldots, \bar{x}_j, \ldots, x_n)
\end{align*}$$

với $x_i, x_j \in \mathbb{F}_2$.
````

````{prf:remark}
:label: quasi-fg

Hàm $f(x_1, \ldots, x_n, y, z)$ là hàm quasi-linear dependent trên biến $y$ và $z$ khi và chỉ khi $f$ có dạng

$$f(x_1, \ldots, x_n, y, z) = g(x_1, \ldots, x_n, y \oplus z) \oplus y.$$
````

```{admonition} **Chứng minh**
:class: danger, dropdown

**Điều kiện cần.** Đặt $\bm{x} = \mathbb{F}_2^n$. Khi đó

$$\begin{align*}
  f(\bm{x}, 0, 0) = g(\bm{x}, 0), \quad f(\bm{x}, 1, 1) = g(\bm{x}, 0) \oplus 1 = \bar{f}(\bm{x}, 0, 0) \\
  f(\bm{x}, 0, 1) = g(\bm{x}, 1), \quad f(\bm{x}, 1, 0) = g(\bm{x}, 1) \oplus 1  = \bar{f}(\bm{x}, 1, 0)
\end{align*}$$

Như vậy $f$ là quasi-linear dependent.

**Điều kiện đủ.** Khai triển $f$ theo $y$ và $z$, sau đó thay $f(\bm{x}, 0, 0)$ bởi $f(\bm{x}, 0, 0) \oplus 1$, tương tự $f(\bm{x}, 0, 1)$ thành $f(\bm{x}, 0, 1) \oplus 1$. Nói cách khác là

$$\begin{align*}
  f(\bm{x}, y, z) & = (y \oplus 1) \cdot (z \oplus 1) \cdot f(\bm{x}, 0, 0) \\
  & \oplus (y \oplus 1) \cdot z \cdot f(\bm{x}, 0, 1) \\
  & \oplus y \cdot (z \oplus 1) \cdot f(\bm{x}, 1, 0) \\
  & \oplus y \cdot z \cdot f(\bm{x}, 1, 1)
\end{align*}$$ (fyz)

Ta gom hai nhóm:

$$\begin{align*}
  & (y \oplus 1) \cdot (z \oplus 1) \cdot f(\bm{x}, 0, 0) \oplus y \cdot z \cdot f(\bm{x}, 1, 1) \\
  = & (yz \oplus y \oplus z \oplus 1) \cdot f(\bm{x}, 0, 0) \oplus y z \cdot (f(\bm{x}, 0, 0) \oplus 1) \\
  = & (y \oplus z \oplus 1) \cdot f(\bm{x}, 0, 0) \oplus yz
\end{align*}$$

$$\begin{align*}
  & (y \oplus 1) \cdot z \cdot f(\bm{x}, 0, 1) \oplus y \cdot (z \oplus 1) \cdot f(\bm{x}, 1, 0) \\
  = & (y \oplus 1) \cdot z \cdot f(\bm{x}, 0, 1) \oplus y \cdot (z \oplus 1) \cdot (f(\bm{x}, 0, 1) \oplus 1) \\
  = & (y \oplus z) \cdot f(\bm{x}, 0, 1) \oplus yz \oplus y
\end{align*}$$

Tóm lại, phương trình khai triển ở {eq}`fyz` sẽ tương đương với

$$f(\bm{x}, y, z) = \underbrace{(y \oplus z \oplus 1) \cdot f(\bm{x}, 0, 0) \oplus (y \oplus z) \cdot f(\bm{x}, 0, 1)}_{g(\bm{x}, y \oplus z)} \oplus y$$
```

````{prf:remark}
Nếu hàm boolean quasi-linear dependent trên hai biến bất kì thì hàm boolean đó cân bằng.
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Đặt $\bm{x} \in \mathbb{F}_2^n$. Do $f(\bm{x}, y, z) \in \mathcal{F}_{n+2}$ và $f$ quasi-linear dependent trên hai biến $y$ và $z$ nên theo {prf:ref}`quasi-fg` thì $f$ có dạng

$$f(\bm{x}, y, z) = g(\bm{x}, y \oplus z) \oplus y$$

Do tổng (XOR) của $f$ có phần tuyến tính nên $f$ cân bằng.

Chúng ta cũng có thể chứng minh theo cách khác bằng khai triển $f$ theo $y$ và $z$

$$\begin{align*}
  f(\bm{x}, y, z) & = y \cdot z \cdot (g(\bm{x}, 0) \oplus 1) \oplus y \cdot (z \oplus 1) \cdot (g(\bm{x}, 1) \oplus 1) \\
  & \oplus (y \oplus 1) \cdot z \cdot g(\bm{x}, 1) \oplus (y \oplus 1) \cdot (z \oplus 1) \cdot g(\bm{x}, 0)
\end{align*}$$

Theo đẳng thức {eq}`wt-decomp` thì

$$\mathrm{wt}(f) = \mathrm{wt}(\bar{g}(\bm{x}, 0)) + \mathrm{wt}(\bar{g}(\bm{x}, 1)) + \mathrm{wt}(g(\bm{x}, 1)) + \mathrm{wt}(g(\bm{x}, 0)) = 2^{n+1}.$$
```

````{prf:example} hàm quasi-linear dependent
Hàm boolean

$$f(x, y, z) = y \oplus xz \oplus xy$$

quasi-linear dependent trên hai biến $y$ và $z$.
````

### Cách tìm đa thức Zhegalkin từ bảng chân trị

Ta có nhiều phương pháp để tìm đa thức Zhegalkin của một hàm boolean từ bảng chân trị. 

#### Phương pháp tam giác

Ở hàng đầu ta viết các phần tử bảng chân trị từ trái sang phải. Với $n$ biến sẽ có $2^n$ ô.

Hàng thứ hai có $2^n-1$ ô. Phần tử dưới sẽ bằng XOR của 2 phần tử ngay trên nó (tạo thành tam giác). Tiếp tục như vậy tới khi ta có hàng cuối chỉ có 1 ô.

```{figure} ../figures/boolean/zhegalkin-1.jpg

Phương pháp tam giác
```

Khi đó, tương ứng với các biến, nếu biến đó là 1 thì hạng tử chứa biến đó, 0 thì không ghi. Ở ví dụ trên, nếu $(x, y) = (0, 0)$  thì không có gì (phần tử 1), $(x, y) = (0, 1)$ tương ứng với hạng tử $y$ trong đa thức Zhegalkin, $(x, y) = (1, 0)$ tương ứng hạng tử $x$. Cuối cùng $(x, y) = (1, 1)$ tương ứng hạng tử $xy$.

Hệ số trước mỗi hạng tử là phần tử đầu tiên bên trái theo bảng kim tự tháp. Như vậy đa thức Zhegalkin là:

$$\begin{equation*}
    f(x, y) = 0 \cdot 1 \oplus 1 \cdot y \oplus 1 \cdot x \oplus 
        1 \cdot xy = x \oplus y \oplus xy
\end{equation*}$$

Đa thức Zhegalkin đóng vai trò quan trọng trong nhiều lĩnh vực, bao gồm cả toán học, vật lý, khoa học máy tính, vì AND và XOR là hai toán tử đại số cơ bản, do đó biểu diễn đa thức Zhegalkin được gọi là dạng chuẩn tắc đại số như ở trên đề cập.

Một ví dụ khác của đa thức Zhegalkin với hàm 3 biến $x$, $y$ và $z$ như hình sau:

```{figure} ../figures/boolean/zhegalkin-2.jpg
```

Như vậy ứng với hàm boolean $f$ thì đa thức Zhegalkin là:

$$\begin{equation*}
    f(x, y, z) = z \oplus yz \oplus x \oplus xz \oplus xyz
\end{equation*}$$

#### Phương pháp Möbius

Phương pháp này cho phép chúng ta tính hệ số đa thức Zhegalkin như phương pháp tam giác nhưng nhanh hơn và đỡ sai sót hơn.

Đầu tiên chúng ta chia đôi bảng chân trị thành hai nửa trái phải. Nửa trái giữa nguyên, mỗi phần tử ở nửa phải được XOR (cộng modulo 2) với phần tử tương ứng ở nửa trái.

Giả sử với hàm $f(x, y) = (0, 1, 1, 1)$ như trên. Bước 1, ta giữ nguyên 2 phần tử đầu 0 và 1. Phần tử thứ ba (mới) bằng phần tử thứ ba (cũ) XOR với phần tử đầu ($0 \oplus 1 = 1$). Phần tử thứ tư (mới) bằng phần tử thứ tư (cũ) XOR với phần tử thứ hai ($1 \oplus 1 = 0$).

Tiếp theo, chúng ta xử lý như trên cho 2 phần tử bên nửa trái (2 phần tử bên nửa phải xử lý tương tự).

```{figure} ../figures/boolean/zhegalkin-3.jpg

Bước 1
```

```{figure} ../figures/boolean/zhegalkin-4.jpg

Bước 2
```

Như vậy ta có kết quả là $(0, 1, 1, 1)$, tương ứng với các hạng tử $1$, $y$, $x$, $xy$ (như trên). Vậy đa thức Zhegalkin là $f(x, y) = x \oplus y \oplus xy$.

