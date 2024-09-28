## Nonlinearlity của hàm boolean

```{contents}
:depth: 2
```

### Biến đổi Fourier

Với mỗi vector $\bm{a} = (a_1, \ldots, a_n) \in \mathbb{F}_2^n$, ta ký hiệu $\langle \bm{a}, \bm{x} \rangle$ là hàm sau:

$$\begin{equation}
	\langle \bm{a}, \bm{x} \rangle = a_1 x_1 \oplus a_2 x_2 \oplus \ldots \oplus a_n x_n
\end{equation}$$ (fur:eq1)

Mỗi hàm boolean $f(\bm{x}) = f(x_1, x_2, \ldots, x_n)$ sẽ được biểu diễn dưới dạng duy nhất với

$$\begin{equation}
	f(\bm{x}) = 2^{-n} \sum_{\bm{a} \in \mathbb{F}_2^n} F_f (\bm{a}) \cdot (-1)^{\langle \bm{a}, \bm{x} \rangle}
\end{equation}$$ (fur:eq2)

Trong đó

$$\begin{equation}
	F_f (\bm{a}) = \sum_{\bm{x} \in \mathbb{F}_2^n} f(\bm{x}) \cdot (-1)^{\langle \bm{a}, \bm{x} \rangle}
\end{equation}$$ (fur:eq3)

Khi đó, tập hợp $\{F_f (\bm{a}), \bm{a} \in \mathbb{F}_2^n \}$ được gọi là **phổ Fourier** (hay **spectre Fourier**) của hàm boolean $f$.

````{prf:remark}
Đầu tiên ta có nhận xét rằng, với vector $\bm{z}$ cố định thì

$$\begin{equation}
    \sum_{\bm{a} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{z} \rangle} = \begin{cases}
        0, \quad & \text{nếu } \bm{z} \neq \bm{0} \\
        2^n, \quad & \text{nếu } \bm{z} = \bm{0}
    \end{cases}
\end{equation}$$ (fur:eq4)
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Để chứng minh nhận xét này, ta thấy rằng nếu $\bm{z} \neq \bm{0}$ thì có ít nhất một bit $z_i \neq 0$. 

Ta chọn vector

$$\Delta = (0, \ldots, 0, 1, 0, \ldots, 0)$$

với bit 1 nằm ở vị trí $i$. Khi đó với mọi vector $\bm{a} \in \mathbb{F}_2^n$ tồn tại duy nhất vector $\bm{a}' \in \mathbb{F}_2^n$ sao cho $\bm{a} \oplus \bm{a}' = \Delta$. 

Suy ra $\langle \bm{a} \oplus \bm{a}', \bm{z} \rangle = \langle \Delta, \bm{z} \rangle = 1$ vì $z_i \cdot 1 = 1$, các vị trí còn lại $z_j \cdot 0 = 0$. 

Lý do ta chọn vector $\Delta$ như vậy là vì

$$\langle \bm{a} \oplus \bm{a}', \bm{z} \rangle = \langle \bm{a}, \bm{z} \rangle \oplus \langle \bm{a}', \bm{z} \rangle = 1.$$

Tương đương với $\langle \bm{a}, \bm{z} \rangle = 1 \oplus \langle \bm{a}', \bm{z} \rangle$. Do đó $\langle \bm{a}, \bm{z} \rangle$ và $\langle \bm{a}', \bm{z} \rangle$ là hai bit khác nhau, dẫn tới $(-1)^{\langle \bm{a}, \bm{z} \rangle}$ và $(-1)^{\langle \bm{a}', \bm{z} \rangle}$ là hai số trái dấu nhau nên tổng chúng là 0. Chúng ta có $2^n / 2$ cặp như vậy và tổng cuối cùng là 0.

Trong trường hợp $\bm{z} = \bm{0}$ thì $\langle \bm{a}, \bm{z} \rangle = \bm{0}$ với mọi $\bm{a} \in \mathbb{F}_2^n$. Do đó $(-1)^{\langle \bm{a}, \bm{z} \rangle} = (-1)^0 = 1$ với mọi vector $\bm{a}$. Hàm boolean $n$ biến có $2^n$ vector $\bm{a}$ nên tổng là $2^n \cdot 1 = 2^n$.
```

Nhận xét {eq}`fur:eq4` đã được chứng minh. Ta quay lại bài toán.

```{admonition} **Chứng minh**
:class: danger, dropdown
Với mọi vector $\bm{x} \in \mathbb{F}_2^n$, ta khai triển từ vế phải của {eq}`fur:eq2` và từ {eq}`fur:eq3`:

$$\begin{align*}
    & 2^{-n} \sum_{\bm{a} \in \mathbb{F}_2^n} F_f (\bm{a}) \cdot (-1)^{\langle \bm{a}, \bm{x} \rangle} \\ = & 2^{-n} \sum_{\bm{a} \in \mathbb{F}_2^n} \biggl( \sum_{\bm{y} \in \mathbb{F}_2^n} f(\bm{y}) \cdot (-1)^{\langle \bm{a}, \bm{y} \rangle} \biggr) \cdot (-1)^{\langle \bm{a}, \bm{x} \rangle} \\ = & 2^{-n} \sum_{\bm{y} \in \mathbb{F}_2^n} f(\bm{y}) \sum_{\bm{a} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{y} \oplus \bm{x} \rangle}
\end{align*}$$

Theo {eq}`fur:eq4`, nếu ta coi $\bm{y} \oplus \bm{x} = \bm{z}$ thì

$$\begin{equation*}
    \sum_{\bm{a} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{y} \oplus \bm{x} \rangle} = \begin{cases}
        0, \quad & \text{nếu } \bm{y} \oplus \bm{x} \neq \bm{0} \\
        2^n, \quad & \text{nếu } \bm{y} \oplus \bm{x} = \bm{0}
    \end{cases}
\end{equation*}$$

Nghĩa là trong tổng trên thì chỉ có $\bm{y}$ thỏa $\bm{y} \oplus \bm{x} = \bm{0}$ thì $f(\bm{y})$ không bị triệt tiêu. Nói cách khác là $\bm{y} = \bm{x}$ và do đó tổng trên còn lại $2^{-n} (f(\bm{x}) \cdot 2^n) = f(\bm{x})$ và ta có điều phải chứng minh.
```

````{prf:example}
Xét hàm boolean $f(x_1, x_2) = (1, 0, 0, 1)$.

Xét $\bm{a} = (0, 0)$. Ta có:

- Với $\bm{x} = (0, 0)$, $f(\bm{x}) = 1$, $\langle \bm{a}, \bm{x} \rangle = 0 \cdot 0 + 0 \cdot 0 = 0$.
- Với $\bm{x} = (0, 1)$, $f(\bm{x}) = 0$, $\langle \bm{a}, \bm{x} \rangle = 0 \cdot 0 + 0 \cdot 1 = 0$
- Với $\bm{x} = (1, 0)$, $f(\bm{x}) = 0$, $\langle \bm{a}, \bm{x} \rangle = 0 \cdot 1 + 0 \cdot 0 = 0$
- Với $\bm{x} = (1, 1)$, $f(\bm{x}) = 1$, $\langle \bm{a}, \bm{x} \rangle = 0 \cdot 1 + 0 \cdot 1 = 0$

Suy ra 

$$F_f (\bm{a}) = 1 \cdot (-1)^0 + 0 \cdot (-1)^0 + 0 \cdot (-1)^0 + 1 \cdot (-1)^0 = 2$$

khi $\bm{a} = (0, 0)$.

Tương tự, ta có các giá trị $F_f (\bm{a})$ sau:

- Với $\bm{a} = (0, 1)$, $F_f (\bm{a}) = F_f (0, 1) = 0$
- Với $\bm{a} = (1, 0)$, $F_f (\bm{a}) = F_f (1, 0) = 0$
- Với $\bm{a} = (1, 1)$, $F_f (\bm{a}) = F_f (1, 1) = 2$

Bây giờ ta đã có đủ $F_f(\bm{a})$ với $\bm{a} \in \mathbb{F}_2^2$ nên ta có thể kiểm chứng với mọi $\bm{x} \in \mathbb{F}_2^2$ thỏa công thức {eq}`fur:eq2`.
````

### Biến đổi Walsh-Hadamard

Với mỗi hàm boolean $f(x_1, x_2, \ldots, x_n) = f(\bm{x})$ ta định nghĩa một hàm tương ứng như sau:

$$f^*(\bm{x}) = (-1)^{f(\bm{x})}$$

Ta định nghĩa $\langle \bm{a}, \bm{x} \rangle$ như trên, khi đó hàm $f^*(\bm{x})$ sẽ có dạng

$$\begin{equation}
	f^*(\bm{x}) = 2^{-n} \sum_{\bm{a} \in \mathbb{F}_2^n} W_f (\bm{a}) (-1)^{\langle \bm{a}, \bm{x} \rangle}
\end{equation}$$ (walsh:eq1)

Trong đó

$$\begin{equation}
	W_f (\bm{a}) = \sum_{\bm{x} \in \mathbb{F}_2^n} (-1)^{f(\bm{x}) \oplus \langle \bm{a}, \bm{x} \rangle}
\end{equation}$$ (walsh:eq2)

Tập hợp $\{ W_f (\bm{a}), \bm{a} \in \mathbb{F}_2^n \}$ được gọi là **phổ Walsh** (hay **spectre Walsh**) của hàm $f(\bm{x})$. Các giá trị $W_f (\bm{a})$ được gọi là hệ số Walsh.
	
```{admonition} **Chứng minh**
:class: danger, dropdown
Tương tự như trên, ta khai triển vế phải của {eq}`walsh:eq1` và thay {eq}`walsh:eq2` vào

$$\begin{align*}
	& 2^{-n} \sum_{\bm{a} \in \mathbb{F}_2^n} W_f (\bm{a}) (-1)^{\langle \bm{a}, \bm{x} \rangle} \\ = & 2^{-n} \sum_{\bm{a} \in \mathbb{F}_2^n} \biggl( \sum_{\bm{y} \in \mathbb{F}_2^n} (-1)^{f(\bm{y}) \oplus \langle \bm{a}, \bm{y} \rangle} \biggr) (-1)^{\langle \bm{a}, \bm{x} \rangle} \\ = & 2^{-n} \sum_{\bm{y} \in \mathbb{F}_2^n} (-1)^{f(\bm{y})} \sum_{\bm{a} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{y} \oplus \bm{x} \rangle}
\end{align*}$$

Cũng từ {eq}`fur:eq4`, tương tự như trên ta có

$$\begin{equation*}
	\sum_{\bm{a} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{y} \oplus \bm{x} \rangle} = \begin{cases}
		0, & \quad \text{nếu } \bm{y} \oplus \bm{x} \neq \bm{0} \\
		2^n, & \quad \text{nếu } \bm{y} \oplus \bm{x} = \bm{0}
	\end{cases}
\end{equation*}$$

Do đó trong các $\bm{y} \in \mathbb{F}_2^n$ thì chỉ có $\bm{y} = \bm{x}$ không bị triệt tiêu nên kết quả là

$$2^{-n} \cdot (-1)^{f(\bm{x})} \cdot 2^n = (-1)^{f(\bm{x})} = f^* (\bm{x}).$$
```

Các hệ số Walsh liên hệ với nhau bởi công thức

$$\begin{equation}
	\sum_{\bm{a} \in \mathbb{F}_2^n} W_f (\bm{a}) W_f (\bm{a} \oplus \bm{d}) = 
	\begin{cases}
		2^{2n}, & \bm{d} = \bm{0} \\
		0, & \bm{d} \neq \bm{0}
	\end{cases}
\end{equation}$$

Trường hợp $\bm{d} = \bm{0}$ được gọi là **đẳng thức Parcel**:

$$\begin{equation}
	\sum_{\bm{a} \in \mathbb{F}_2^n} (W_f (\bm{a}))^2 = 2^{2n}
\end{equation}$$

### Tính chất của biến đổi Walsh-Hadamard

1. $W_f(\bm{0}) = 2^n - 2 \mathrm{wt} (f)$, và $W_f(\bm{0}) = 0$ khi và chỉ khi $f$ là hàm cân bằng.
2. Nếu $g = \bar{f}$ thì $W_g(\bm{a}) = -W_f(\bm{a})$ với mọi $\bm{a} \in \mathbb{F}_2^n$.
3. Nếu $g(\bm{x}) = f(\bm{x} \oplus \bm{b})$ với vector $\bm{b}$ nào đó, thì

$$\begin{align*}
	W_g(\bm{a}) & = \sum_x (-1)^{f(\bm{x} \oplus \bm{b}) \oplus \langle \bm{a}, \bm{x} \rangle} \\
	& = \sum_x (-1)^{f(\bm{x}) \oplus \langle \bm{a}, \bm{x} \oplus \bm{b} \rangle} \\
	& = (-1)^{\langle \bm{a}, \bm{b} \rangle W_f(\bm{a})}
\end{align*}$$

4. Đặt $f \in \mathcal{F}_n$, $\bm{b} \in \mathbb{F}_2^n$, $g(\bm{x}) = f(\bm{x}) \oplus \langle \bm{b}, \bm{x} \rangle$. Khi đó

$$\begin{align*}
	W_g(\bm{a}) & = \sum_x (-1)^{f(\bm{x}) \oplus \langle \bm{b}, \bm{x} \rangle \oplus \langle \bm{a}, \bm{x} \rangle} \\
	& = \sum_x (-1)^{f(\bm{x}) \oplus \langle \bm{b} \oplus \bm{a}, \bm{x} \rangle} \\
	& = W_f(\bm{b} \oplus \bm{a})
\end{align*}$$

5. Đặt $f(\bm{x}) = c$ là hằng số. Hàm $c \oplus \langle \bm{a}, \bm{x} \rangle$ là hàm tuyến tính với mọi $\bm{a} \neq \bm{0}$. Hệ quả là $W_f(\bm{a}) = 0$ với mọi vector $\bm{a}$ khác không, trừ khi

$$W_f(\bm{0}) = 2^n - 2 \mathrm{wt} (f) = \begin{cases}
	- 2^n, & \, \text{nếu} \, c = 1, \\
	\quad 2^n, & \, \text{nếu} \, c = 0.
\end{cases}$$

6. Đặt $f(\bm{x}) = c \oplus \langle \bm{b}, \bm{x} \rangle$ là hàm affine. Khi đó, theo tính chất 4 và 5 suy ra $W_f(\bm{a}) = 0$ với mọi $\bm{a} \neq \bm{0}$, và $W_f(\bm{b}) = (-1)^c \cdot 2^n$.
7. Đặt $f(\bm{x}, \bm{y}) = g(\bm{x}) \oplus h(\bm{y})$ với $g \in \mathcal{F}_n$ và $h \in \mathcal{F}_m$ và hai tập hợp biến $\bm{x}$ và $\bm{y}$ không giao nhau. Nói cách khác $f$ là hàm boolean $n+m$ biến. Khi đó với mọi $\bm{a} \in \mathbb{F}_2^n$ và $\bm{b} \in \mathbb{F}_2^n$ thì

$$\begin{align*}
	W_f(\bm{a} \bm{b}) & = \sum_{\bm{x}, \bm{y}} (-1)^{g(\bm{x}) \oplus h(\bm{y}) \oplus \langle \bm{a}, \bm{x} \rangle \oplus \langle \bm{b}, \bm{y} \rangle} \\
	& = \sum_{\bm{x}} (-1)^{g(\bm{x}) \oplus \langle \bm{a}, \bm{x} \rangle} \sum_{\bm{y}} (-1)^{h(\bm{y}) \oplus \langle \bm{b}, \bm{y} \rangle} \\
	& = W_g(\bm{a}) \cdot W_h(\bm{b})
\end{align*}$$

8. Đặt $f(x_1, \ldots, x_n)$ *giả phụ thuộc* vào biến $x_i$. Khi đó $W_f(\bm{a}) = 0$ với mọi vector $\bm{a}$ mà $a_i = 1$.

Nói cách khác, nếu đặt $\bm{x}' = (x_1, \ldots, x_{i-1}, x_{i+1}, \ldots, x_n)$ và $\bm{a}' = (a_1, \ldots, a_{i-1}, a_{i+1}, \ldots, a_n)$ và để ý rằng $\langle \bm{a}, \bm{x} \rangle = \langle \bm{a}', \bm{x}' \rangle \oplus a_i x_i$. Khi đó nếu $a_i = 1$ thì

$$\begin{align*}
	W_f(\bm{a}) & = \sum_\bm{x} (-1)^{f(\bm{x}) \oplus \langle \bm{a}, \bm{x} \rangle} \\ 
	& = \sum_{\substack{\bm{x}, \\ x_i = 0}} (-1)^{f(\bm{x}) \oplus \langle \bm{a}', \bm{x}' \rangle} + \sum_{\substack{\bm{x}, \\ x_i = 1}} (-1)^{f(\bm{x}) \oplus \langle \bm{a}', \bm{x}' \rangle \oplus 1} = 0
\end{align*}$$

### Liên hệ giữa hệ số Fourier và hệ số Walsh

````{prf:remark}
Quan hệ giữa hệ số Fourier và hệ số Walsh là biểu thức sau

$$\begin{equation}
	W_f (\bm{a}) = 2^n \Delta (\bm{a}) - 2 F_f (\bm{a})
\end{equation}$$

với $\Delta (\bm{a}) = \begin{cases}
	1, \quad \text{nếu } \bm{a} = \bm{0} \\
	0, \quad \text{nếu } \bm{a} \neq \bm{0}
\end{cases}$
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Ta có

$$\begin{align*}
	W_f (\bm{a}) + 2 F_f (\bm{a}) = & \sum_{\bm{x} \in \mathbb{F}_2^n} (-1)^{f(\bm{x}) \oplus \langle \bm{a}, \bm{x} \rangle} + 2 \sum_{\bm{x} \in \mathbb{F}_2^n} f(\bm{x}) (-1)^{\langle \bm{a}, \bm{x} \rangle} \\ = & \sum_{\bm{x} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{x} \rangle} [(-1)^{f(\bm{x})} + 2 f(\bm{x})]
\end{align*}$$

Để ý rằng, nếu $f(\bm{x}) = 0$ thì

$$(-1)^{f(\bm{x})} + 2 f(\bm{x}) = (-1)^0 + 2 \cdot 0 = 1,$$

còn nếu $f(\bm{x}) = 1$ thì

$$(-1)^{f(\bm{x})} + 2 f(\bm{x}) = (-1)^1 + 2 \cdot 1 = 1.$$

Nói cách khác biểu thức trên trở thành

$$W_f (\bm{a}) + 2 F_f (\bm{a}) = \sum_{\bm{x} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{x} \rangle}$$

Từ {eq}`fur:eq2` ta có

$$\sum_{\bm{x} \in \mathbb{F}_2^n} (-1)^{\langle \bm{a}, \bm{x} \rangle} = \begin{cases}
	0, \quad &\text{nếu } \bm{a} \neq \bm{0} \\ 2^n, \quad & \text{nếu } \bm{a} = \bm{0}
\end{cases}$$

Như vậy nếu đặt $\Delta(\bm{a}) = \begin{cases}
	1, \text{nếu } \bm{a} = \bm{0} \\ 0, \text{nếu } \bm{a} \neq \bm{0}
\end{cases}$ thì ta có điều phải chứng minh.
```
	
````{prf:remark}
Khi $\bm{a} = \bm{0}$ thì với mọi $\bm{x} \in \mathbb{F}_2^n$ ta đều có $\langle \bm{a}, \bm{x} \rangle = 0$. Do đó

$$F_f (\bm{0}) = \sum_{\bm{x} \in \mathbb{F}_2^n} f(\bm{x}) (-1)^{\langle \bm{a}, \bm{x} \rangle} = \sum_{\bm{x} \in \mathbb{F}_2^n} f(\bm{x}) (-1)^0 = \mathrm{wt}(f)$$

Suy ra

$$\begin{equation}
	W_f (\bm{0}) = 2^n - 2 wt(f) \Leftrightarrow wt(f) = 2^{n-1} - \frac{1}{2} W_f (\bm{0})
\end{equation}$$ (walsh:eq4)
````

### Hàm Bent

Ta ký hiệu $\mathcal{A}$ là tập hợp tất cả các hàm boolean affine với $n$ biến. Nghĩa là

$$\begin{equation}
	\mathcal{A} = \{ a_0 \oplus a_1 x_1 \oplus \cdots \oplus a_n x_n \, | \, a_0, a_1, \ldots, a_n \in \mathbb{F}_2 \}
\end{equation}$$

````{prf:definition} Nonlinearity của hàm boolean
**Nonlinearity** của hàm boolean $f$ bất kì được định nghĩa là khoảng cách Hamming từ $f$ tới $\mathcal{A}$, hay nói cách khác $N_f = d(f, \mathcal{A})$.
````

````{prf:remark}
Xét hàm $f$ với $n$ biến và phổ Walsh tương ứng của hàm $f$ là $\{ W_f (\bm{a}), \bm{a} \in \mathbb{F}_2^n \}$. Khi đó 

$$\begin{equation}
	N_f = 2^{n-1} - \frac{1}{2} \max_{\bm{a} \in \mathbb{F}_2^n} \lvert W_f (\bm{a}) \rvert
\end{equation}$$ (walsh:eq3)
````

````{prf:remark}
Từ đẳng thức Parcel ta có

$$\begin{align*}
	& 2^n \cdot \bigl(\max_{\bm{a} \in \mathbb{F}_2^n} (W_f (\bm{a}))^2\bigr) \geqslant \sum_{\bm{a} \in \mathbb{F}_2^n} (W_f (\bm{a}))^2 = 2^{2n} \\ \Leftrightarrow & \max_{\bm{a} \in \mathbb{F}_2^n} (W_f (\bm{a}))^2 \geqslant \frac{2^{2n}}{2^n} = 2^n \\ \Leftrightarrow & \max_{\bm{a} \in \mathbb{F}_2^n} \lvert W_f (\bm{a}) \rvert \geqslant 2^{n/2}
\end{align*}$$
````

Từ nhận xét trên và từ định nghĩa nonlinearity ở trên ta có

$$N_f \leqslant 2^{n-1} - \frac{1}{2} 2^{n / 2}$$

Hàm $f$ khiến dấu bằng xảy ra được gọi là **hàm Bent**. Điều kiện cần và đủ để hàm $f$ có $n$ biến là hàm Bent là khi $n = 2k$.

Tính chất quan trọng của hàm Bent là với mọi vector $\bm{a}$ thì

$$W_f (\bm{a}) = \pm 2^{n/2}$$

````{prf:example}
Với $n = 2$, hàm $f(x_1, x_2) = x_1 \oplus x_1 x_2$ là hàm Bent. Ta có thể tính toán và thấy rằng $W_f (0, 0) = 2$, $W_f (0, 1) = -2$, $W_f (1, 0) = 2$ và $W_f (1, 1) = 2$.
````
