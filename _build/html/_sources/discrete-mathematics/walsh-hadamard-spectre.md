## Nonlinearlity của hàm boolean

```{contents}
:depth: 2
```

### Biến đổi Fourier

Với mỗi vector $\mathbf{a} = (a_1, \ldots, a_n) \in \mathbb{F}_2^n$, ta ký hiệu $\langle \mathbf{a}, \mathbf{x} \rangle$ là hàm sau:

$$\begin{equation}
	\langle \mathbf{a}, \mathbf{x} \rangle = a_1 x_1 \oplus a_2 x_2 \oplus \ldots \oplus a_n x_n
\end{equation}$$ (fur:eq1)

Mỗi hàm boolean $f(\mathbf{x}) = f(x_1, x_2, \ldots, x_n)$ sẽ được biểu diễn dưới dạng duy nhất với

$$\begin{equation}
	f(\mathbf{x}) = 2^{-n} \sum_{\mathbf{a} \in \mathbb{F}_2^n} F_f (\mathbf{a}) \cdot (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle}
\end{equation}$$ (fur:eq2)

Trong đó

$$\begin{equation}
	F_f (\mathbf{a}) = \sum_{\mathbf{x} \in \mathbb{F}_2^n} f(\mathbf{x}) \cdot (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle}
\end{equation}$$ (fur:eq3)

Khi đó, tập hợp $\{F_f (\mathbf{a}), \mathbf{a} \in \mathbb{F}_2^n \}$ được gọi là **phổ Fourier** (hay **spectre Fourier**) của hàm boolean $f$.

````{prf:remark}
Đầu tiên ta có nhận xét rằng, với vector $\mathbf{z}$ cố định thì

$$\begin{equation}
    \sum_{\mathbf{a} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{z} \rangle} = \begin{cases}
        0, \quad & \text{nếu } \mathbf{z} \neq \mathbf{0} \\
        2^n, \quad & \text{nếu } \mathbf{z} = \mathbf{0}
    \end{cases}
\end{equation}$$ (fur:eq4)
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Để chứng minh nhận xét này, ta thấy rằng nếu $\mathbf{z} \neq \mathbf{0}$ thì có ít nhất một bit $z_i \neq 0$. 

Ta chọn vector

$$\Delta = (0, \ldots, 0, 1, 0, \ldots, 0)$$

với bit 1 nằm ở vị trí $i$. Khi đó với mọi vector $\mathbf{a} \in \mathbb{F}_2^n$ tồn tại duy nhất vector $\mathbf{a}' \in \mathbb{F}_2^n$ sao cho $\mathbf{a} \oplus \mathbf{a}' = \Delta$. 

Suy ra $\langle \mathbf{a} \oplus \mathbf{a}', \mathbf{z} \rangle = \langle \Delta, \mathbf{z} \rangle = 1$ vì $z_i \cdot 1 = 1$, các vị trí còn lại $z_j \cdot 0 = 0$. 

Lý do ta chọn vector $\Delta$ như vậy là vì

$$\langle \mathbf{a} \oplus \mathbf{a}', \mathbf{z} \rangle = \langle \mathbf{a}, \mathbf{z} \rangle \oplus \langle \mathbf{a}', \mathbf{z} \rangle = 1.$$

Tương đương với $\langle \mathbf{a}, \mathbf{z} \rangle = 1 \oplus \langle \mathbf{a}', \mathbf{z} \rangle$. Do đó $\langle \mathbf{a}, \mathbf{z} \rangle$ và $\langle \mathbf{a}', \mathbf{z} \rangle$ là hai bit khác nhau, dẫn tới $(-1)^{\langle \mathbf{a}, \mathbf{z} \rangle}$ và $(-1)^{\langle \mathbf{a}', \mathbf{z} \rangle}$ là hai số trái dấu nhau nên tổng chúng là 0. Chúng ta có $2^n / 2$ cặp như vậy và tổng cuối cùng là 0.

Trong trường hợp $\mathbf{z} = \mathbf{0}$ thì $\langle \mathbf{a}, \mathbf{z} \rangle = \mathbf{0}$ với mọi $\mathbf{a} \in \mathbb{F}_2^n$. Do đó $(-1)^{\langle \mathbf{a}, \mathbf{z} \rangle} = (-1)^0 = 1$ với mọi vector $\mathbf{a}$. Hàm boolean $n$ biến có $2^n$ vector $\mathbf{a}$ nên tổng là $2^n \cdot 1 = 2^n$.
```

Nhận xét {eq}`fur:eq4` đã được chứng minh. Ta quay lại bài toán.

```{admonition} **Chứng minh**
:class: danger, dropdown
Với mọi vector $\mathbf{x} \in \mathbb{F}_2^n$, ta khai triển từ vế phải của {eq}`fur:eq2` và từ {eq}`fur:eq3`:

$$\begin{align*}
    & 2^{-n} \sum_{\mathbf{a} \in \mathbb{F}_2^n} F_f (\mathbf{a}) \cdot (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} \\ = & 2^{-n} \sum_{\mathbf{a} \in \mathbb{F}_2^n} \biggl( \sum_{\mathbf{y} \in \mathbb{F}_2^n} f(\mathbf{y}) \cdot (-1)^{\langle \mathbf{a}, \mathbf{y} \rangle} \biggr) \cdot (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} \\ = & 2^{-n} \sum_{\mathbf{y} \in \mathbb{F}_2^n} f(\mathbf{y}) \sum_{\mathbf{a} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{y} \oplus \mathbf{x} \rangle}
\end{align*}$$

Theo {eq}`fur:eq4`, nếu ta coi $\mathbf{y} \oplus \mathbf{x} = \mathbf{z}$ thì

$$\begin{equation*}
    \sum_{\mathbf{a} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{y} \oplus \mathbf{x} \rangle} = \begin{cases}
        0, \quad & \text{nếu } \mathbf{y} \oplus \mathbf{x} \neq \mathbf{0} \\
        2^n, \quad & \text{nếu } \mathbf{y} \oplus \mathbf{x} = \mathbf{0}
    \end{cases}
\end{equation*}$$

Nghĩa là trong tổng trên thì chỉ có $\mathbf{y}$ thỏa $\mathbf{y} \oplus \mathbf{x} = \mathbf{0}$ thì $f(\mathbf{y})$ không bị triệt tiêu. Nói cách khác là $\mathbf{y} = \mathbf{x}$ và do đó tổng trên còn lại $2^{-n} (f(\mathbf{x}) \cdot 2^n) = f(\mathbf{x})$ và ta có điều phải chứng minh.
```

````{prf:example}
Xét hàm boolean $f(x_1, x_2) = (1, 0, 0, 1)$.

Xét $\mathbf{a} = (0, 0)$. Ta có:

- Với $\mathbf{x} = (0, 0)$, $f(\mathbf{x}) = 1$, $\langle \mathbf{a}, \mathbf{x} \rangle = 0 \cdot 0 + 0 \cdot 0 = 0$.
- Với $\mathbf{x} = (0, 1)$, $f(\mathbf{x}) = 0$, $\langle \mathbf{a}, \mathbf{x} \rangle = 0 \cdot 0 + 0 \cdot 1 = 0$
- Với $\mathbf{x} = (1, 0)$, $f(\mathbf{x}) = 0$, $\langle \mathbf{a}, \mathbf{x} \rangle = 0 \cdot 1 + 0 \cdot 0 = 0$
- Với $\mathbf{x} = (1, 1)$, $f(\mathbf{x}) = 1$, $\langle \mathbf{a}, \mathbf{x} \rangle = 0 \cdot 1 + 0 \cdot 1 = 0$

Suy ra 

$$F_f (\mathbf{a}) = 1 \cdot (-1)^0 + 0 \cdot (-1)^0 + 0 \cdot (-1)^0 + 1 \cdot (-1)^0 = 2$$

khi $\mathbf{a} = (0, 0)$.

Tương tự, ta có các giá trị $F_f (\mathbf{a})$ sau:

- Với $\mathbf{a} = (0, 1)$, $F_f (\mathbf{a}) = F_f (0, 1) = 0$
- Với $\mathbf{a} = (1, 0)$, $F_f (\mathbf{a}) = F_f (1, 0) = 0$
- Với $\mathbf{a} = (1, 1)$, $F_f (\mathbf{a}) = F_f (1, 1) = 2$

Bây giờ ta đã có đủ $F_f(\mathbf{a})$ với $\mathbf{a} \in \mathbb{F}_2^2$ nên ta có thể kiểm chứng với mọi $\mathbf{x} \in \mathbb{F}_2^2$ thỏa công thức {eq}`fur:eq2`.
````

### Biến đổi Walsh-Hadamard

Với mỗi hàm boolean $f(x_1, x_2, \ldots, x_n) = f(\mathbf{x})$ ta định nghĩa một hàm tương ứng như sau:

$$f^*(\mathbf{x}) = (-1)^{f(\mathbf{x})}$$

Ta định nghĩa $\langle \mathbf{a}, \mathbf{x} \rangle$ như trên, khi đó hàm $f^*(\mathbf{x})$ sẽ có dạng

$$\begin{equation}
	f^*(\mathbf{x}) = 2^{-n} \sum_{\mathbf{a} \in \mathbb{F}_2^n} W_f (\mathbf{a}) (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle}
\end{equation}$$ (walsh:eq1)

Trong đó

$$\begin{equation}
	W_f (\mathbf{a}) = \sum_{\mathbf{x} \in \mathbb{F}_2^n} (-1)^{f(\mathbf{x}) \oplus \langle \mathbf{a}, \mathbf{x} \rangle}
\end{equation}$$ (walsh:eq2)

Tập hợp $\{ W_f (\mathbf{a}), \mathbf{a} \in \mathbb{F}_2^n \}$ được gọi là **phổ Walsh** (hay **spectre Walsh**) của hàm $f(\mathbf{x})$. Các giá trị $W_f (\mathbf{a})$ được gọi là hệ số Walsh.
	
```{admonition} **Chứng minh**
:class: danger, dropdown
Tương tự như trên, ta khai triển vế phải của {eq}`walsh:eq1` và thay {eq}`walsh:eq2` vào

$$\begin{align*}
	& 2^{-n} \sum_{\mathbf{a} \in \mathbb{F}_2^n} W_f (\mathbf{a}) (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} \\ = & 2^{-n} \sum_{\mathbf{a} \in \mathbb{F}_2^n} \biggl( \sum_{\mathbf{y} \in \mathbb{F}_2^n} (-1)^{f(\mathbf{y}) \oplus \langle \mathbf{a}, \mathbf{y} \rangle} \biggr) (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} \\ = & 2^{-n} \sum_{\mathbf{y} \in \mathbb{F}_2^n} (-1)^{f(\mathbf{y})} \sum_{\mathbf{a} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{y} \oplus \mathbf{x} \rangle}
\end{align*}$$

Cũng từ {eq}`fur:eq4`, tương tự như trên ta có

$$\begin{equation*}
	\sum_{\mathbf{a} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{y} \oplus \mathbf{x} \rangle} = \begin{cases}
		0, & \quad \text{nếu } \mathbf{y} \oplus \mathbf{x} \neq \mathbf{0} \\
		2^n, & \quad \text{nếu } \mathbf{y} \oplus \mathbf{x} = \mathbf{0}
	\end{cases}
\end{equation*}$$

Do đó trong các $\mathbf{y} \in \mathbb{F}_2^n$ thì chỉ có $\mathbf{y} = \mathbf{x}$ không bị triệt tiêu nên kết quả là

$$2^{-n} \cdot (-1)^{f(\mathbf{x})} \cdot 2^n = (-1)^{f(\mathbf{x})} = f^* (\mathbf{x}).$$
```

Các hệ số Walsh liên hệ với nhau bởi công thức

$$\begin{equation}
	\sum_{\mathbf{a} \in \mathbb{F}_2^n} W_f (\mathbf{a}) W_f (\mathbf{a} \oplus \mathbf{d}) = 
	\begin{cases}
		2^{2n}, & \mathbf{d} = \mathbf{0} \\
		0, & \mathbf{d} \neq \mathbf{0}
	\end{cases}
\end{equation}$$

Trường hợp $\mathbf{d} = \mathbf{0}$ được gọi là **đẳng thức Parcel**:

$$\begin{equation}
	\sum_{\mathbf{a} \in \mathbb{F}_2^n} (W_f (\mathbf{a}))^2 = 2^{2n}
\end{equation}$$

### Liên hệ giữa hệ số Fourier và hệ số Walsh

````{prf:remark}
Quan hệ giữa hệ số Fourier và hệ số Walsh là biểu thức sau

$$\begin{equation}
	W_f (\mathbf{a}) = 2^n \Delta (\mathbf{a}) - 2 F_f (\mathbf{a})
\end{equation}$$

với $\Delta (\mathbf{a}) = \begin{cases}
	1, \quad \text{nếu } \mathbf{a} = \mathbf{0} \\
	0, \quad \text{nếu } \mathbf{a} \neq \mathbf{0}
\end{cases}$
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Ta có

$$\begin{align*}
	W_f (\mathbf{a}) + 2 F_f (\mathbf{a}) = & \sum_{\mathbf{x} \in \mathbb{F}_2^n} (-1)^{f(\mathbf{x}) \oplus \langle \mathbf{a}, \mathbf{x} \rangle} + 2 \sum_{\mathbf{x} \in \mathbb{F}_2^n} f(\mathbf{x}) (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} \\ = & \sum_{\mathbf{x} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} [(-1)^{f(\mathbf{x})} + 2 f(\mathbf{x})]
\end{align*}$$

Để ý rằng, nếu $f(\mathbf{x}) = 0$ thì

$$(-1)^{f(\mathbf{x})} + 2 f(\mathbf{x}) = (-1)^0 + 2 \cdot 0 = 1,$$

còn nếu $f(\mathbf{x}) = 1$ thì

$$(-1)^{f(\mathbf{x})} + 2 f(\mathbf{x}) = (-1)^1 + 2 \cdot 1 = 1.$$

Nói cách khác biểu thức trên trở thành

$$W_f (\mathbf{a}) + 2 F_f (\mathbf{a}) = \sum_{\mathbf{x} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle}$$

Từ {eq}`fur:eq2` ta có

$$\sum_{\mathbf{x} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} = \begin{cases}
	0, \quad &\text{nếu } \mathbf{a} \neq \mathbf{0} \\ 2^n, \quad & \text{nếu } \mathbf{a} = \mathbf{0}
\end{cases}$$

Như vậy nếu đặt $\Delta(\mathbf{a}) = \begin{cases}
	1, \text{nếu } \mathbf{a} = \mathbf{0} \\ 0, \text{nếu } \mathbf{a} \neq \mathbf{0}
\end{cases}$ thì ta có điều phải chứng minh.
```
	
````{prf:remark}
Khi $\mathbf{a} = \mathbf{0}$ thì với mọi $\mathbf{x} \in \mathbb{F}_2^n$ ta đều có $\langle \mathbf{a}, \mathbf{x} \rangle = 0$. Do đó

$$F_f (\mathbf{0}) = \sum_{\mathbf{x} \in \mathbb{F}_2^n} f(\mathbf{x}) (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} = \sum_{\mathbf{x} \in \mathbb{F}_2^n} f(\mathbf{x}) (-1)^0 = \mathrm{wt}(f)$$

Suy ra

$$\begin{equation}
	W_f (\mathbf{0}) = 2^n - 2 wt(f) \Leftrightarrow wt(f) = 2^{n-1} - \frac{1}{2} W_f (\mathbf{0})
\end{equation}$$ (walsh:eq4)
````

### Hàm Bent

Ta ký hiệu $\mathcal{A}$ là tập hợp tất cả các hàm boolean affine với $n$ biến. Nghĩa là

$$\begin{equation}
	\mathcal{A} = \{ a_0 \oplus a_1 x_1 \oplus \cdots \oplus a_n x_n \, | \, a_0 a_1, \ldots, a_n \in \mathbb{F}_2 \}
\end{equation}$$

````{prf:definition} Nonlinearity của hàm boolean
**Nonlinearity** của hàm boolean $f$ bất kì được định nghĩa là khoảng cách Hamming từ $f$ tới $\mathcal{A}$, hay nói cách khác $N_f = d(f, \mathcal{A})$.
````

````{prf:remark}
Xét hàm $f$ với $n$ biến và phổ Walsh tương ứng của hàm $f$ là $\{ W_f (\mathbf{a}), \mathbf{a} \in \mathbb{F}_2^n \}$. Khi đó 

$$\begin{equation}
	N_f = 2^{n-1} - \frac{1}{2} \max_{\mathbf{a} \in \mathbb{F}_2^n} \lvert W_f (\mathbf{a}) \rvert
\end{equation}$$ (walsh:eq3)
````

````{prf:remark}
Từ đẳng thức Parcel ta có

$$\begin{align*}
	& 2^n \cdot \bigl(\max_{\mathbf{a} \in \mathbb{F}_2^n} (W_f (\mathbf{a}))^2\bigr) \geqslant \sum_{\mathbf{a} \in \mathbb{F}_2^n} (W_f (\mathbf{a}))^2 = 2^{2n} \\ \Leftrightarrow & \max_{\mathbf{a} \in \mathbb{F}_2^n} (W_f (\mathbf{a}))^2 \geqslant \frac{2^{2n}}{2^n} = 2^n \\ \Leftrightarrow & \max_{\mathbf{a} \in \mathbb{F}_2^n} \lvert W_f (\mathbf{a}) \rvert \geqslant 2^{n/2}
\end{align*}$$
````

Từ nhận xét trên và từ định nghĩa nonlinearity ở trên ta có

$$N_f \leqslant 2^{n-1} - \frac{1}{2} 2^{n / 2}$$

Hàm $f$ khiến dấu bằng xảy ra được gọi là **hàm Bent**. Điều kiện cần và đủ để hàm $f$ có $n$ biến là hàm Bent là khi $n = 2k$.

Tính chất quan trọng của hàm Bent là với mọi vector $\mathbf{a}$ thì

$$W_f (\mathbf{a}) = \pm 2^{n/2}$$

````{prf:example}
Với $n = 2$, hàm $f(x_1, x_2) = x_1 \oplus x_1 x_2$ là hàm Bent. Ta có thể tính toán và thấy rằng $W_f (0, 0) = 2$, $W_f (0, 1) = -2$, $W_f (1, 0) = 2$ và $W_f (1, 1) = 2$.
````
