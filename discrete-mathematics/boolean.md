# Đại số boolean

```{contents}
```

Boolean (hay luận lý) chỉ giá trị đúng hoặc sai của mệnh đề nào đó. 

Theo cách hiểu cơ bản, boolean gồm hai giá trị 0 hoặc 1 (sai hoặc đúng). Chương này tham khảo chính từ {cite}`Tokareva1`, {cite}`Tokareva2` và {cite}`Pank14`.

Một số kí hiệu hay dùng:

1. Để chỉ tập hợp tất cả hàm boolean $n$ biến ta dùng $\mathcal{F}_n$.
2. Để chỉ tập hợp tất cả hàm boolean affine $n$ biến ta dùng $\mathcal{A}_n$.
3. Để chỉ tập hợp tất cả hàm boolean tuyến tính $n$ biến ta dùng $\mathcal{L}_n$.

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
