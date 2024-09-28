## Hàm boolean

```{contents}
```

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
Xét hai vector $\bm{a} = (a_1, a_2, \ldots, a_n)$ và $\bm{b} = (b_1, b_2, \ldots, b_n)$ ($a_i, b_i \in \{0, 1\}$). Ta nói $\bm{a}$ **so sánh được nhỏ hơn** $\bm{b}$ nếu với mọi $i = 1, 2, \ldots, n$ ta có $a_i \leqslant b_i$. Ký hiệu $\bm{a} \prec \bm{b}$.
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

#### Một số kí hiệu hay dùng

1. Để chỉ tập hợp tất cả hàm boolean $n$ biến ta dùng $\mathcal{F}_n$.
2. Để chỉ tập hợp tất cả hàm boolean affine $n$ biến ta dùng $\mathcal{A}_n$.
3. Để chỉ tập hợp tất cả hàm boolean tuyến tính $n$ biến ta dùng $\mathcal{L}_n$.

Ở trên đã tính được

$$\lvert \mathcal{F}_n \rvert = 2^{2^n}.$$

Số lượng hàm boolean affine là số cách chọn các hệ số $a_0$, $a_1$, ..., $a_n$. Như vậy cần chọn $n+1$ số trong $\mathbb{F}_2$ nên

$$\lvert \mathcal{A}_n \rvert = 2^{n+1}.$$

Đối với hàm boolean tuyến tính thì chọn từ $a_1$ tới $a_n$ nên cần chọn $n$ số, suy ra

$$\lvert \mathcal{L}_n \rvert = 2^n.$$
