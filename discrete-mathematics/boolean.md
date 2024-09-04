# Đại số boolean

```{contents}
```

Boolean (hay luận lý) chỉ giá trị đúng hoặc sai của mệnh đề nào đó. 

Theo cách hiểu cơ bản, boolean gồm hai giá trị 0 hoặc 1 (sai hoặc đúng). Chương này tham khảo chính từ {cite}`Tokareva1` và {cite}`Tokareva2`.

## Hàm boolean

Hàm boolean $f$ đối với các biến $x_1, x_2, \ldots, x_n$ là hàm số nhận giá trị trong $\mathbb{F}_2^n$ và trả về giá trị thuộc $\mathbb{F}_2$.

Nói cách khác $f$ là ánh xạ từ $\mathbb{F}_2^n$ tới $\mathbb{F}_2$.

Ta ký hiệu hàm boolean $n$ biến là $f(x_1, x_2, \ldots, x_n)$.

Do $x_i \in \mathbb{F}_2$ nên ta có $2^n$ vector (bộ số) $(x_1, x_2, \ldots, x_n)$. Giá trị của hàm $f$ lại nằm trong tập $\{0, 1\}$ nên ứng với mỗi vector có thể có 2 giá trị của hàm boolean, và ta có $2^n$ vector nên số lượng hàm boolean có thể có là $2^{2^n}$.

Một số toán tử boolean hay dùng: đối, AND, OR, XOR, NAND, NOR, kéo theo, tương đương.

Để biểu diễn hàm boolean chúng ta dùng bảng chân trị. Bảng chân
trị tương ứng với các toán tử boolean trên là:

| | | AND | OR | XOR | NAND | NOR |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| $x_1$ | $x_2$ | $x_1 \cdot x_2$ | $x_1 \vee x_2$ | $x_1 \oplus x_2$ | $x_1 \vert x_2$ | $x_1 \downarrow x_2$ |
| 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 | 1 | 1 | 0 |
| 1 | 1 | 1 | 1 | 0 | 0 | 0 |

Toán tử đối làm đổi giá trị của hàm bool (0 thành 1 và 1 thành 0).
Ký hiệu $\overline{x}$.

```{list-table} Toán tử đối
:header-rows: 1

* - $x$
  - $\overline{x}$
* - 0
  - 1
* - 1
  - 0
```

```{list-table} Toán tử kéo theo và tương đương
:header-rows: 1

* - $x_1$
  - $x_2$
  - $x_1 \rightarrow x_2$ 
  - $x_1 \sim x_2$
* - 0 
  - 0 
  - 1
  - 1
* - 0
  - 1 
  - 1 
  - 0
* - 1 
  - 0 
  - 0 
  - 0
* - 1
  - 1 
  - 1 
  - 1
```

Toán tử tương đương còn chỉ sự tương đương của hai mệnh đề logic.
Khi hai biểu thức logic có cùng bảng chân trị thì hai mệnh đề đó
tương đương nhau. Do đó ta có thể viết một số kết quả như sau (từ
các bảng chân trị cơ bản trên):

- $x_1 \vert x_2 \sim \overline{x_1 \cdot x_2}$. Ở đây ta đổi dấu từng giá trị hàm boolean $x_1 \cdot x_2$
- $x_1 \downarrow x_2 \sim \overline{x_1 \vee x_2}$. Tương tự ta đổi dấu từng giá trị hàm boolean $x_1 \vee x_2$

### Đa thức Zhegalkin

````{prf:definition} Đa thức Zhegalkin
Với hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$, **đa thức Zhegalkin** tương ứng với hàm bool đó là cách biểu diễn đa thức đó dưới dạng tổng các tích như sau

$$\begin{equation}
    f(x_1, x_2, \ldots, x_n) = a_0 \oplus a_1 x_1 
    \oplus a_2 x_2 \oplus a_3 x_1 x_2 \oplus \ldots 
    \oplus a_k x_1 x_2 \ldots x_n
\end{equation}$$

với $a_i \in \{0, 1\}$. Ta thấy rằng có $n$ biến, do đó có $2^n$ hệ số $a_i$ ($i = 0, 1, \ldots, 2^n-1$).
````

Khi đó ta nói hàm boolean $f$ được biểu diễn ở **dạng chuẩn tắc đại số** (hay **algebraic normal form**, **ANF**).

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

````{prf:definition} Bậc của đa thức Zhegalkin
Tương tự như bậc của một đa thức đại số thông thường, bậc của đa thức Zhegalkin là bậc của hạng tử chứa nhiều đơn thức $x_i$ nhất. Ký hiệu là $\deg(f)$.
````

````{prf:example}
Xét hàm boolean $f(x, y, z) = 1 \oplus x \oplus yz \oplus xyz$. Khi đó $\deg(f) = 3$ vì hạng tử chứa nhiều đơn thức nhất là $xyz$ có 3 đơn thức.

Xét hàm boolean $f(x, y, z) = 1 \oplus z \oplus zy \oplus xy$. Khi đó $\deg(f) = 2$ vì hạng tử chứa nhiều đơn thức nhất là $zy$ (cũng có thể xét $xy$).
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

### Hàm affine và hàm tuyến tính

````{prf:definition} Hàm boolean affine
Xét hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$. Khi đó $f$ được gọi là **hàm boolean affine** nếu nó có dạng

$$\begin{equation}
    f(x_1, x_2, \ldots, x_n) = a_0 \oplus a_1 x_1 \oplus 
    a_2 x_2 \oplus \ldots \oplus a_n x_n
\end{equation}$$

Khi $a_0 = 0$ thì ta gọi là **hàm boolean tuyến tính** (linear).
````

Ta thấy rằng chỉ có các hạng tử dạng $a_i x_i$ xuất hiện trong biểu diễn đa thức Zhegalkin tương ứng của hàm boolean đó. Hay  nói cách khác hàm boolean là affine khi $\deg(f) = 1$.

````{prf:example}
Hàm boolean $f(x, y) = x \oplus y$ là hàm boolean affine và cũng tuyến tính. Hàm boolean $f(x, y) = x \oplus xy$ không là hàm boolean affine.
````

Tiếp theo ta sẽ xét sự so sánh của hai vector và hàm boolean đơn điệu.

### Hàm đơn điệu

````{prf:definition} Vector so sánh được
Xét hai vector $\mathbf{a} = (a_1, a_2, \ldots, a_n)$ và $\mathbf{b} = (b_1, b_2, \ldots, b_n)$ ($a_i, b_i \in \{0, 1\}$). Ta nói $\mathbf{a}$ **so sánh được nhỏ hơn** $\mathbf{b}$ nếu với mọi $i = 1, 2, \ldots, n$ ta có $a_i \leqslant b_i$. Ký hiệu $\mathbf{a} \prec \mathbf{b}$.
````

````{prf:example}
Ta có $(1, 0, 0) \prec (1, 0, 1)$, còn $(1, 0, 0)$ và $(0, 1, 0)$
thì không so sánh được (vị trí thứ 1 và thứ 2).
````

````{prf:definition} Hàm boolean đơn điệu
Hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$ được gọi là **hàm boolean đơn điệu** (hay **monotone**) nếu với mọi vector $(a_1, a_2, \ldots, a_n) \prec (b_1, b_2, \ldots, b_n)$ thì ta có 

$$\begin{equation}
    f(a_1, a_2, \ldots, a_n) \leqslant f(b_1, b_2, \ldots, b_n)  
\end{equation}$$
````

````{prf:example}
Xét hàm boolean $f(x, y) = (0, 1, 0, 1)$.

Ta thấy rằng:
- $(0, 0) \prec (0, 1)$ và $f(0, 0) = 0 \leqslant 1 = f(0, 1)$
- $(0, 0) \prec (1, 0)$ và $f(0, 0) = 0 \leqslant 0 = f(1, 0)$
- $(0, 0) \prec (1, 1)$ và $f(0, 0) = 0 \leqslant 1 = f(1, 1)$
- $(0, 1)$ và $(1, 0)$ không so sánh được nên bỏ qua
- $(0, 1) \prec (1, 1)$ và $f(0, 1) = 1 \leqslant 1 = f(1, 1)$
- $(1, 0) \prec (1, 1)$ và $f(1, 0) = 0 \leqslant 1 = f(1, 1)$

Vậy đây là hàm đơn điệu.
````

## Trọng số, phổ Furier, phổ Walsh, Hamming distance

Ở phần này ký hiệu vector không $\mathbf{0} = (0, \ldots, 0)$, vector một $\mathbf{1} = (1, \ldots, 1)$.

### Trọng số của hàm boolean

````{prf:definition} Trọng số hàm boolean
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

```{admonition} **Chứng minh.**
:class: danger, dropdown
Để chứng minh nhận xét này, ta thấy rằng nếu $\mathbf{z} \neq \mathbf{0}$ thì có ít nhất một bit $z_i \neq 0$. 

Ta chọn vector $\Delta = (0, \ldots, 0, 1, 0, \ldots, 0)$ với bit 1 nằm ở vị trí $i$. Khi đó với mọi vector $\mathbf{a} \in \mathbb{F}_2^n$ tồn tại duy nhất vector $\mathbf{a}' \in \mathbb{F}_2^n$ sao cho $\mathbf{a} \oplus \mathbf{a}' = \Delta$. 

Suy ra $\langle \mathbf{a} \oplus \mathbf{a}', \mathbf{z} \rangle = \langle \Delta, \mathbf{z} \rangle = 1$ vì $z_i \cdot 1 = 1$, các vị trí còn lại $z_j \cdot 0 = 0$. 

Lý do ta chọn vector $\Delta$ như vậy là vì $\langle \mathbf{a} \oplus \mathbf{a}', \mathbf{z} \rangle = \langle \mathbf{a}, \mathbf{z} \rangle \oplus \langle \mathbf{a}', \mathbf{z} \rangle = 1$. Tương đương với $\langle \mathbf{a}, \mathbf{z} \rangle = 1 \oplus \langle \mathbf{a}', \mathbf{z} \rangle$. Do đó $\langle \mathbf{a}, \mathbf{z} \rangle$ và $\langle \mathbf{a}', \mathbf{z} \rangle$ là hai bit khác nhau, dẫn tới $(-1)^{\langle \mathbf{a}, \mathbf{z} \rangle}$ và $(-1)^{\langle \mathbf{a}', \mathbf{z} \rangle}$ là hai số trái dấu nhau nên tổng chúng là 0. Chúng ta có $2^n / 2$ cặp như vậy và tổng cuối cùng là 0.

Trong trường hợp $\mathbf{z} = \mathbf{0}$ thì $\langle \mathbf{a}, \mathbf{z} \rangle = \mathbf{0}$ với mọi $\mathbf{a} \in \mathbb{F}_2^n$. Do đó $(-1)^{\langle \mathbf{a}, \mathbf{z} \rangle} = (-1)^0 = 1$ với mọi vector $\mathbf{a}$. Hàm boolean $n$ biến có $2^n$ vector $\mathbf{a}$ nên tổng là $2^n \cdot 1 = 2^n$.
```

Nhận xét {eq}`fur:eq4` đã được chứng minh. Ta quay lại bài toán.

```{admonition} **Chứng minh.**
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

Suy ra $F_f (\mathbf{a}) = 1 \cdot (-1)^0 + 0 \cdot (-1)^0 + 0 \cdot (-1)^0 + 1 \cdot (-1)^0 = 2$ khi $\mathbf{a} = (0, 0)$.

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
	
```{admonition} **Chứng minh.**
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

Do đó trong các $\mathbf{y} \in \mathbb{F}_2^n$ thì chỉ có $\mathbf{y} = \mathbf{x}$ không bị triệt tiêu nên kết quả là $2^{-n} \cdot (-1)^{f(\mathbf{x})} \cdot 2^n = (-1)^{f(\mathbf{x})} = f^* (\mathbf{x})$.
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

```{admonition} **Chứng minh.**
:class: danger, dropdown
Ta có

$$\begin{align*}
	W_f (\mathbf{a}) + 2 F_f (\mathbf{a}) = & \sum_{\mathbf{x} \in \mathbb{F}_2^n} (-1)^{f(\mathbf{x}) \oplus \langle \mathbf{a}, \mathbf{x} \rangle} + 2 \sum_{\mathbf{x} \in \mathbb{F}_2^n} f(\mathbf{x}) (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} \\ = & \sum_{\mathbf{x} \in \mathbb{F}_2^n} (-1)^{\langle \mathbf{a}, \mathbf{x} \rangle} [(-1)^{f(\mathbf{x})} + 2 f(\mathbf{x})]
\end{align*}$$

Để ý rằng, nếu $f(\mathbf{x}) = 0$ thì $(-1)^{f(\mathbf{x})} + 2 f(\mathbf{x}) = (-1)^0 + 2 \cdot 0 = 1$, còn nếu $f(\mathbf{x}) = 1$ thì $(-1)^{f(\mathbf{x})} + 2 f(\mathbf{x}) = (-1)^1 + 2 \cdot 1 = 1$. Nói cách khác biểu thức trên trở thành

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

### Hàm Bent

Ta ký hiệu $\mathcal{L}$ là tập hợp tất cả các hàm boolean affine với $n$ biến. Nghĩa là

$$\begin{equation}
	\mathcal{L} = \{ l_{a_0} (\mathbf{a}, \mathbf{x}) \, | \, a_0 \in \mathbb{F}_2, \mathbf{a} \in \mathbb{F}_2^n \}
\end{equation}$$

với $l_{a_0} (\mathbf{a}, \mathbf{x}) = a_0 \oplus a_1 x_1 \oplus \ldots \oplus a_n x_n$.

````{prf:definition} Nonlinearity của hàm boolean
**Nonlinearity** của hàm boolean $f$ bất kì được định nghĩa là khoảng cách Hamming từ $f$ tới $\mathcal{L}$, hay nói cách khác $N_f = d(f, \mathcal{L})$.
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

## Linear Feedback Shift Register

Linear Feedback Shift Register (LFSR) là một ứng dụng quan trọng của hàm boolean để sinh ra một chuỗi các giá trị (giả ngẫu nhiên, pseudorandom).

### Linear Feedback Shift Register

Xét hàm boolean $n$ biến $f(x_0, x_1, \ldots, x_{n-1})$. Khi đó với các giá trị (bit) khởi tạo $x_0$, $x_1$, ..., $x_{n-1}$ thuộc $\mathbb{F}_2$, ta có thể sinh ra bit ở các vị trí tiếp theo

$$x_{n} = f(x_0, x_1, \ldots, x_{n-1})$$

Tương tự, $x_{n+1} = f(x_1, x_2, \ldots, x_n)$, $x_{n+2} = f(x_2, x_3, \ldots, x_{n+1})$, $x_{n+3} = f(x_3, x_4, \ldots, x_{n+2})$, ...

Tổng quát, để sinh bit thứ $n+i$ thì đầu vào sẽ là các bit $x_i$, $x_{i+1}$, ..., $x_{i+n-1}$.

$$\begin{equation}
	x_{n+i} = f(x_i, x_{i+1}, \ldots, x_{i+n-1})
\end{equation}$$

Theo hình sau ({numref}`lfsr:im1`), kết quả của hàm $f$ sẽ được nối vào sau của dãy bit. Theo đó dãy bit sẽ luôn có dạng $x_0$, $x_1$, ..., $x_n$, ...

```{figure} ../figures/boolean/lfsr-1.jpg
:name: lfsr:im1

Feedback Shift Register
```

Thông qua hàm $f$, các vector trong $\mathbb{F}_2^n$ sẽ chuyển trạng thái lẫn nhau theo công thức 

$$\begin{equation}
	(x_{n-1}, x_{n-2}, \ldots, x_1, x_0) \to (x_n, x_{n-1}, \ldots, x_2, x_1)
\end{equation}$$

````{prf:example}
Xét hàm boolean $f(x_3, x_2, x_1, x_0) = x_3 x_2 \oplus x_0$. Bảng chân trị của hàm $f$ là

$$f(x_3, x_2, x_1, x_0) = (0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1, 0, 1, 0)$$

Ví dụ, với $(0, 0, 0, 1)$, ta có $f(0, 0, 0, 1) = 1$ nên $(0, 0, 0, 1)$ biến đổi thành $(1, 0, 0, 0)$. Như vậy chúng ta có các chuyển đổi đối với hàm $f$ được thể hiện thành 4 chu trình ở các hình sau.

<!-- %\[(0, 0, 0, 0) \to (0, 0, 0, 0)\] -->

<!-- %\[(0, 0, 0, 1) \to (1, 0, 0, 0) \to (0, 1, 0, 0) \to (0, 0, 1, 0) \to (0, 0, 0, 1)\] -->

<!-- %\[(0, 0, 1, 1) \to (1, 0, 0, 1) \to (1, 1, 0, 0) \to (1, 1, 1, 0) \to (1, 1, 1, 1) \to (0, 1, 1, 1) \to (1, 0, 1, 1) \to (1, 1, 0, 1) \to (0, 1, 1, 0) \to (0, 0, 1, 1)\] -->

<!-- %\[(0, 1, 0, 1) \to (1, 0, 1, 0) \to (0, 1, 0, 1)\] -->

```{figure} ../figures/boolean/lfsr-2.jpg

Chu trình thứ nhất của $f$
```

```{figure} ../figures/boolean/lfsr-3.jpg

Chu trình thứ hai của $f$
```

```{figure} ../figures/boolean/lfsr-4.jpg

Chu trình thứ ba của $f$
```

```{figure} ../figures/boolean/lfsr-5.jpg

Chu trình thứ tư của $f$
```
````

Ta thấy rằng tập các vector $\mathbf{x} = (x_i, x_{i+1}, \ldots, x_{i+n-1})$ có $2^n$ trường hợp. Do đó sẽ có một lúc nào đó (số $i$ nào đó) mà vector $\mathbf{x}$ trở lại đúng vector ban đầu. Nghĩa là tồn tại $i$ sao cho

$$(x_0, x_1, \ldots, x_{n-1}) = (x_i, x_{i+1}, \ldots, x_{i+n-1})$$

Từ đó dãy bit tiếp theo được sinh ra sẽ giống hệt trước đó nên số $i$ nhỏ nhất thỏa mãn đẳng thức được gọi là **chu kì** của Feedback Shift Register.

Trong các hàm boolean thì hàm boolean tuyến tính được quan tâm nhiều nhất để sinh ra chuỗi bit Feedback Shift Register. Do đó từ đây ta tập trung vào các hàm boolean tuyến tính và Linear Feedback Shift Register.

Nhắc lại, hàm boolean tuyến tính là hàm boolean có dạng

$$\begin{equation*}
	f(x_0, x_1, \ldots, x_{n-1}) = a_0 x_0 \oplus a_1 x_1 \oplus \ldots \oplus a_{n-1} x_{n-1}
\end{equation*}$$

Trong đó $a_i \in \mathbb{F}_2$ là các hệ số cho trước. Ta định nghĩa đa thức đặc trưng cho hàm boolean tuyến tính như sau.

````{prf:definition} Đa thức đặc trưng
Xét hàm boolean tuyến tính

$$f(x_0, x_1, \ldots, x_{n-1}) = a_0 x_0 \oplus a_1 x_1 \oplus \ldots \oplus a_{n-1} x_{n-1}$$

Khi đó đa thức đặc trưng tương ứng với hàm $f$ là đa thức trong $\mathrm{GF}(2^n)$

$$\begin{equation}
	P(x) = a_0 + a_1 x + \ldots + a_{n-1} x^{n-1} + x^n
\end{equation}$$
````

Do hàm boolean tuyến tính có tính chất là $f(\mathbf{0}) = 0$ nên chu kì tối đa có thể đạt được là $2^n - 1$. Ta có một vài định nghĩa sau để một LFSR đạt được chu kì tối đa.

````{prf:definition} Đa thức primitive
Xét đa thức $P(x) = a_0 + a_1 x + \ldots + a_{n-1} x^{n-1} + x^n$ thuộc $\mathrm{GF}(2^n)$. Ta đã biết trường $\mathrm{GF}(2^n)$ có $2^n - 1$ phần tử khác không. Đặt $p = 2^n - 1$. Đa thức $P(x)$ được gọi là **primitive** khi với mọi ước nguyên tố $q$ của $p$ thì:

$$\begin{equation*}
	x^s \not\equiv 1 \bmod{P(x)}, \quad \text{với} \ s = \frac{p}{q} = \frac{2^n - 1}{q}
\end{equation*}$$
````

````{prf:definition} Đa thức đặc trưng với chu kì cực đại
Đa thức $P(x) = a_0 + a_1 x + \ldots + a_{n-1} x^{n-1} + x^n$ được gọi là **đa thức đặc trưng với chu kì cực đại** nếu đa thức đó tối giản và là đa thức primitive. 
````

````{prf:example}
Xét đa thức $f(x) = x^4 + x^3 + 1$. Ta có thể xác định xem đa thức này có sinh ra LFSR với chu kì tối đa hay không mà không cần tìm đồ thị chuyển trạng thái của LFSR.

Đầu tiên ta chứng minh $f(x)$ là đa thức tối giản. Thật vậy, giả sử ngược lại, $f(x)$ là tích của hai đa thức bậc nhỏ hơn 4. Hai trường hợp có thể xảy ra là $f(x)$ chia hết cho đa thức tối giản bậc 1 hoặc bậc 2.

Các đa thức tối giản bậc 1 là $x$ và $x+1$. Ta có thể kiểm chứng rằng $f(x)$ không chia hết cho bất kì đa thức nào ở trên. Tương tự, đa thức tối giản bậc 2 (trong $\mathrm{GF}(2^4)$) là $x^2 + x + 1$ và $f(x)$ cũng không chia hết cho đa thức này. Như vậy ta có thể kết luận rằng $f(x)$ là đa thức tối giản.

Trong $\mathrm{GF}(2^4)$ có $2^4 - 1 = 15$ phần tử khác 0. Các ước nguyên tố của 15 là 3 và 5. Ta thấy rằng $x^3 \not\equiv 1$ và $x^5 = x \cdot x^4 = x \cdot (x^3 + 1) = x^4 + x = x^3 + x + 1 \not\equiv 1$. Như vậy $f(x)$ là đa thức primitive.

Như vậy ta có thể kết luận rằng đa thức $f(x)$ sinh ra LFSR với chu kì tối đa.
````

### Thuật toán Berlekamp-Massey

Thuật toán Berlekamp-Massey là thuật toán tìm đa thức sinh có chu kì ngắn nhất sinh ra một dãy LFSR cho trước.

Bài toán ở đây là, giả sử chúng ta có một dãy bit

$$\begin{equation*}
	u_0, u_1, \ldots, u_{l-1}
\end{equation*}$$

là một dãy bit được sinh giả ngẫu nhiêu (pseudorandom). Làm thế nào từ đoạn bit này ta xây dựng được đa thức đặc trưng của LFSR mà sinh ra tất cả các bit sau đó? Hơn nữa $l$ phải nhỏ nhất có thể.

Nhắc lại, đa thức đặc trưng là đa thức có dạng

$$\begin{equation*}
	P(x) = a_0 + a_1 x + \ldots + a_{n-1} x^{n-1} + a_n x^n
\end{equation*}$$

thì hàm boolean tuyến tính sinh ra bit tiếp theo sẽ có dạng

$$\begin{equation*}
	x_n = f(x_0, x_1, \ldots, x_{n-1}) = a_0 x_0 \oplus a_1 x_1 \oplus \ldots \oplus a_{n-1} x_{n-1}
\end{equation*}$$

Tổng quát, công thức để sinh ra bit thứ $n+i$ sẽ là

$$\begin{equation*}
	x_{n+i} = f(x_i, x_{i+1}, \ldots, x_{n+i-1}) = a_0 x_i \oplus a_1 x_{i+1} \oplus \ldots \oplus a_{n-1} x_{n+i-1} 
\end{equation*}$$

với $i=0, 1, \ldots$.

````{prf:algorithm} Thuật toán Berlekamp-Massey

Đầu vào là dãy bit $u_0, u_1, \ldots, u_{l-1}$. 

Đầu ra là đa thức đặc trưng bậc nhỏ nhất mà sinh ra toàn bộ dãy bit trên, bắt đầu từ các bit $u_0, u_1, \ldots$ nhất định.

**Bước -1.** Gọi $n_0$ là vị trí đầu tiên mà $u_{n_0} = 1$ (các bit được đánh số từ 0). Khi đó đặt $P_{-1}(x) = 1$ và $k_{-1} = 1$. Nếu $P_{-1}(x)$ sinh ra toàn bộ dãy bit thì ta dừng thuật toán. Ngược lại thì tiếp tục bước 1.

**Bước 0.** Đặt $P_0(x) = x^{n_0 + 1} \oplus P_{-1}(x)$ với $n_0$ là vị trí bit 1 đầu tiên và đặt $k_0 = \deg P_0(x) = n_0 + 1$.

Ở mỗi bước từ đây trở đi, gọi $m$ là số sao cho $k_{-1} = k_0 = \ldots = k_{m-1} < k_{m} = k_{s+2} = \ldots$.

**Bước $n$.** Để tìm $P_n(x)$ ta tính $a = m - k_{m-1}$ và $b = n - k_{n-1}$.

Nếu $a \geqslant b$ thì $P_n(x) = P_{n-1}(x) \oplus x^{a-b} P_{m-1}(x)$.

Nếu $a < b$ thì $P_n(x) = x^{b-a} P_{n-1}(x) \oplus P_{m-1}$.

Trong quá trình tìm $P_n(x)$, khi nào bậc $k_n$ của $P_n(x)$ thỏa mãn điều kiện số $m$ thì ta cập nhật lại số $m$.

Ở mỗi bước, nếu $P_n(x)$ sinh ra toàn bộ dãy bit thì ta dừng thuật toán.
````

````{prf:example}
Xét dãy bit $111100100$. Đặt $n_0 = 0$, $P_{-1}(x) = 1$ và $k_{-1} = 0$.

Theo $P_{-1}(x) = 1$ thì $1 \to 1 \to 1 \to 1$, nghĩa là bit đầu thành bit thứ hai, bit thứ hai thành bit thứ ba và thứ ba thành thứ tư. Từ đó suy ra

$$\begin{equation*}
	P_0 (x) = P_1 (x) = P_2 (x) = P_3 (x) = x^{0+1} \oplus 1 = x \oplus 1.
\end{equation*}$$

Do $k_{-1} < k_0 = k_1 = k_2 = k_3$ (0 < 1) nên $m = 0$.

Để tìm $P_4(x)$, ta có $a =  m- k_{m-1} = 0 - 0 = 0$ và $b = n - k_{n-1} = 4 - 1 = 3$. Do $a < b$ nên

$$\begin{equation*}
	P_4(x) = x^3 P_3(x) \oplus P_{-1}(x) = x^3 \cdot (x \oplus 1) \oplus 1 = x^4 \oplus x^3 \oplus 1.
\end{equation*}$$

Do $k_4 > k_3$ (4 > 1) nên $m = 4$.

```{figure} ../figures/berlekamp_massey-1.jpg

LFSR tương ứng $P_4(x)$
```

Trong hình trên, hàng đầu từ trái sang phải là $u_0, u_1, u_2, u_3$. Hàng thứ hai từ trái sang phải là $u_1, u_2, u_3, u_4$. Hàng thứ ba là $u_2, u_3, u_4, u_5$ nhưng $u_5 = 0$ theo dãy ban đầu nên LFSR sinh ra 1 là chưa đúng, thuật toán chuyển sang bước tiếp theo.

Để tìm $P_5(x)$, ta có $a = m - k_{m-1} = 4 - 1 = 3$ và $b = n - k_{n-1} = 5 - 4 = 1$. Suy ra

$$\begin{equation*}
	P_5(x) = P_4(x) \oplus x^2 P_3 (x) = x^4 \oplus x^3 \oplus 1 \oplus x^2 \cdot (x \oplus 1) = x^4 \oplus x^2 \oplus 1.
\end{equation*}$$

Theo $P_5(x) = x^4 \oplus x^2 \oplus 1$ thì LFSR sẽ hoạt động như hình dưới đây. Cũng theo hình dưới thì $P_6(x) = P_5(x) = x^4 \oplus x^2 \oplus 1$. 
	
```{figure} ../figures/berlekamp_massey-2.jpg

LFSR tương ứng $P_5(x)$ và $P_6(x)$
```

Để tìm $P_7(x)$, ta có $a = m - k_{m-1} = 3$ và $b = n - k_{n-1} = 7 - 4 = 3$. Do $a \geqslant b$ nên

$$\begin{equation*}
	P_7(x) = P_6(x) \oplus P_3(x) = x^4 \oplus x^2 \oplus 1 \oplus x \oplus 1 = x^4 \oplus x^2 \oplus x.
\end{equation*}$$

Khi đó LFSR sẽ được sinh như hình.

```{figure} ../figures/berlekamp_massey-3.jpg

LFSR tương ứng $P_7(x)$
```

Để tìm $P_8(x)$, $a = 3$ và $b = 8 - 4 = 4$. Do $a < b$ nên

$$\begin{equation*}
	P_8(x) = x P_7(x) \oplus P_3(x) = x^5 \oplus x^3 \oplus x^2 \oplus x \oplus 1.
\end{equation*}$$

Lúc này LFSR sẽ là

```{figure} ../figures/berlekamp_massey-4.jpg

LFSR tương ứng $P_8(x)$
```

Như vậy đa thức sinh ra dãy bit ban đầu là $x^5 \oplus x^3 \oplus x^2 \oplus x \oplus 1$. Thuật toán Berlekamp-Massey tìm ra đa thức đặc trưng với độ phức tạp là 8 (tìm tới $P_8(x)$).
````

Ví dụ trên có thể được kiểm tra bởi chương trình Python [ở đây](https://github.com/dunglq2000/lfsr-berlekamp-massey).