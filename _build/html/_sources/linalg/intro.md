# Ma trận

```{contents}
:depth: 2
```

Trong các bài viết của về đại số tuyến tính:

1. Vector sẽ được ký hiệu bởi chữ thường in đậm (ví dụ $\mathbf{v}, \mathbf{x}, \ldots$)​; 
2. Ma trận sẽ được ký hiệu bởi chữ hoa in đậm (ví dụ $\mathbf{A},\ \mathbf{B}, \ldots$​);
3. Các đại lượng vô hướng (số) được ký hiệu bởi chữ thường không in đậm (ví dụ $x_1,\ N,\ t, \ldots$).

Bảng thuật ngữ và ký hiệu

| Ký hiệu | Ý nghĩa |
| ------- | ------- |
| $\mathbf{A}^T$ | Ma trận chuyển vị (transpose) của ma trận $\mathbf{A}$ |
| $\mathbf{A}^{-1}$ | Ma trận nghịch đảo (inverse) của ma trận $\mathbf{A}$ |
| $\text{rank} \ \mathbf{A}$ | Hạng (rank) của ma trận $\mathbf{A}$ |
| $\det \mathbf{A}$ | Định thức (determinant) ma trận $\mathbf{A}$ |
| $\mathbf{x} \cdot \mathbf{y}$ | Tích vô hướng hai vector $\mathbf{x}$ và $\mathbf{y}$ |
| $\dim \mathcal{V}$ | Số chiều (dimension) không gian vector $\mathcal{V}$ |
| $\lVert \mathbf{x} \rVert$ | Chuẩn Euclid (Euclidean norm) vector $\mathbf{x}$ |

## Định thức, ma trận nghịch đảo, hạng ma trận

### Định thức ma trận

````{prf:definition} Nghịch thế
Cho tập hợp $A = \{1, 2, \cdots, n\}$ và xét hoán vị $\sigma$ trên ​$A$. Ta gọi hai phần tử $i$​ và $j$​ tạo thành **nghịch thế** (hay **inversion**) nếu $i < j$​ và $\sigma(i) > \sigma(j)$.

Đặt $\sigma = \begin{pmatrix}
    1 & 2 & \ldots & n \\
    k_1 & k_2 & \cdots & k_n
\end{pmatrix}$​ là một hoán vị của $A$​. Ta ký hiệu $P(\sigma)$ là số lượng nghịch thế của $\sigma$​ và đặt $(-1)^{P(\sigma)} = \text{sign} \ \sigma$.
````

````{prf:example}
Với $n=4$​, $A = \{1, 2, 3, 4\}$​. Xét hoán vị $\sigma = \begin{pmatrix} 1 & 2 & 3 & 4 \\ 4 & 2 & 1 & 3\end{pmatrix}$.

Ta nhận thấy các cặp nghịch thế $(1, 2),\ (1, 3),\ (1, 4),\ (2, 3)$​ gồm bốn cặp nghịch thế. Vậy $P(\sigma) = 4$ và $\text{sign} \ \sigma=(-1)^4=1$​.
````

````{prf:definition} Định thức
Khi đó **định thức** của ma trận $\mathbf{A} = \begin{pmatrix}a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \cdots & \cdots & \cdots & \cdots \\ a_{n1} & a_{n2} & \cdots & a_{nn}\end{pmatrix}$ được định nghĩa là:

$$\begin{equation}
    \det(\mathbf{A})=\displaystyle{\sum_{(i_1, i_2, \cdots, i_n)} a_{1, i_1} \cdot a_{2, i_2} \cdot a_{n, i_n} \cdot \text{sign} \sigma}
\end{equation}$$

với mọi hoán vị $\sigma = \begin{pmatrix}1 & 2 & \ldots & n \\ i_1 & i_2 & \cdots & i_n \end{pmatrix}$ của tập $\{ 1, 2, \cdots, n \}$. Như vậy có $n!$​ phần tử cho tổng trên.
````

````{prf:example}
Tính định thức ma trận $\mathbf{A}=\begin{pmatrix}1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9\end{pmatrix}$​.

Xét hoán vị $\sigma_1 = \begin{pmatrix} 1 & 2 & 3 \\ 1 & 2 & 3 \end{pmatrix}$​. Khi đó $P(\sigma_1)=0$​, $a_{11} \cdot a_{22} \cdot a_{33} \cdot (-1)^0 = 1 \cdot 5 \cdot 9 \cdot 1 = 45$​.

Xét hoán vị $\sigma_2 = \begin{pmatrix} 1 & 2 & 3 \\ 1 & 3 & 2 \end{pmatrix}$​. Khi đó $P(\sigma_2) = 1$​, $a_{11} \cdot a_{23} \cdot a_{32} \cdot (-1)^1 = 1 \cdot 6 \cdot 8 \cdot (-1) = -48$.

Xét hoán vị $\sigma_3 = \begin{pmatrix} 1 & 2 & 3 \\ 2 & 1 & 3 \end{pmatrix}$​. Khi đó $P(\sigma_3) = 1$​, $a_{12} \cdot a_{21} \cdot a_{33} \cdot (-1)^1 = 2 \cdot 4 \cdot 9 \cdot (-1) = -72$.

Xét hoán vị $\sigma_4 = \begin{pmatrix} 1 & 2 & 3 \\ 2 & 3 & 1 \end{pmatrix}$. Khi đó $P(\sigma_4) = 2$​, $a_{12} \cdot a_{23} \cdot a_{31} \cdot (-1)^2 = 2 \cdot 6 \cdot 7 \cdot 1 = 84$​.

Xét hoán vị $\sigma_5 = \begin{pmatrix} 1 & 2 & 3 \\ 3 & 1 & 2 \end{pmatrix}$. Khi đó $P(\sigma_5) = 2$​, $a_{13} \cdot a_{21} \cdot a_{32} \cdot (-1)^2 = 3 \cdot 4 \cdot 8 \cdot 1 = 96$​.

Xét hoán vị $\sigma_6 = \begin{pmatrix} 1 & 2 & 3 \\ 3 & 2 & 1 \end{pmatrix}$​. Khi đó $P(\sigma_6) = 3$​, $a_{13} \cdot a_{22} \cdot a_{31} \cdot (-1)^3 = 3 \cdot 5 \cdot 7 \cdot  (-1) = -105$​.

Như vậy $\det(A)=45-48-72+84+96-105=0$​.
````

Định thức của ma trận còn được định nghĩa theo **đệ quy** như sau:

Với ma trận $1 \times 1$ là $\mathbf{A}=\begin{pmatrix}a_{11}\end{pmatrix}$ thì $\det(\mathbf{A})=a_{11}$.

Với ma trận $2 \times 2$ là $\mathbf{A} = \begin{pmatrix}a_{11} & a_{12} \\ a_{21} & a_{22}\end{pmatrix}$​ thì $\det(\mathbf{A})=a_{11}a_{22} - a_{21}a_{12}$.

Với ma trận $n \times n$, gọi $\mathbf{M}_{ij}$ là ma trận có được từ ma trận $\mathbf{A}$ khi bỏ đi hàng $i$​ và cột $j$​ của ma trận $\mathbf{A}$ và ký hiệu $A_{ij}=(-1)^{i+j} \det (\mathbf{M}_{ij})$. Khi đó:

````{prf:theorem} Định lý Laplace
Định lý Laplace cho phép ta khai triển định thức của ma trận cấp $n$ thành tổng các ma trận cấp $n-1$.

Khai triển theo cột $j$​:

$$\det(\mathbf{A})=\displaystyle{\sum_{i=1}^na_{ij} A_{ij}} = a_{1j} A_{1j} + a_{2j} A_{2j} + \cdots + a_{nj} A_{nj},\ j = \overline{1, n}.$$

Khai triển theo hàng $i$​: 

$$\det(\mathbf{A})=\displaystyle{\sum_{j=1}^n a_{ij} A_{ij}} = a_{i1} A_{i1} + a_{i2} A_{i2} + \cdots + a_{in} A_{in},\ i = \overline{1, n}. $$
````

### Ma trận nghịch đảo

````{prf:definition} Ma trận nghịch đảo
Ma trận $\mathbf{A}^{-1}$​ được gọi là **ma trận nghịch đảo** của ma trận vuông $\mathbf{A}$ nếu $\mathbf{A}^{-1} \cdot \mathbf{A} = \mathbf{A} \cdot \mathbf{A}^{-1} = \mathbf{I}$​. Trong đó $\mathbf{I}$ là ma trận đơn vị cùng kích thước với $\mathbf{A}$.
````

$$\begin{equation}
    \mathbf{A}^{-1}=\frac{1}{\det(\mathbf{A})}[(A_{ij})_n]^T=\frac{1}{\det(\mathbf{A})}\begin{pmatrix} A_{11} & A_{21} & \cdots & A_{n1} \\ A_{12} & A_{22} & \cdots & A_{n2} \\ \cdots & \cdots & \cdots & \cdots \\ A_{1n} & A_{2n} & \cdots & A_{nn} \end{pmatrix}
\end{equation}$$

Trong đó, $A_{ij}$ cũng được định nghĩa tương tự như khi tính định thức bằng khai triển theo dòng hoặc cột. Gọi $\mathbf{M}_{ij}$ là ma trận có được từ ma trận $\mathbf{A}$ khi bỏ đi hàng $i$​ và cột $j$​ của ma trận $\mathbf{A}$ và ký hiệu $A_{ij}=(-1)^{i+j} \det (\mathbf{M}_{ij})$.

Như vậy, điều kiện cần và đủ để một ma trận có nghịch đảo là định thức khác 0.

### Hạng của ma trận

````{prf:definition} Hạng của ma trận
Cho ma trận $\mathbf{A}_{m \times n}$. **Hạng** của ma trận là cấp của ma trận con lớn nhất có định thức khác 0.
````

Nghĩa là, một ma trận vuông mà là ma trận con (lấy một phần của ma trận ban đầu) kích thước $r \times r$ mà có định thức khác 0 và $r$ lớn nhất, thì hạng của ma trận khi đó là $r$. 

````{prf:remark}
Ma trận con kích thước $r \times r$ là ma trận con của ma trận kích thước $m \times n$ nên $r \leqslant \min(m, n)$.
````

````{prf:example}
Ma trận $\mathbf{A} = \begin{pmatrix}
    1 & 2 & 3 \\ 2 & 4 & 6 \\ 1 & 2 & 4
\end{pmatrix}$ có định thức $\det(\mathbf{A}) = 0$. 

Nhưng ma trận con của $\mathbf{A}$ là $\mathbf{B} = \begin{pmatrix}2 & 3 \\ 2 & 4\end{pmatrix}$ (lấy dòng 1 và 3, lấy cột 2 và 3) có định thức $\det(\mathbf{B}) = 2 \neq 0$, do đó $r = \text{rank} \ (\mathbf{A}) = 2$ ($\text{rank} \ (\mathbf{A})$ nghĩa là hạng của $\mathbf{A}$).
````


## Tổ hợp tuyến tính

Xét tập hợp các vector $\{\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d\}$ trên $\mathbb{R}$.

````{prf:definition} Tổ hợp tuyến tính
Với vector $\mathbf{x}$ bất kì thuộc $\mathbb{R}$, nếu tồn tại các số thực $\alpha_1, \alpha_2, \ldots, \alpha_d \in \mathbb{R}$ sao cho

$$\mathbf{x} = \alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \ldots + \alpha_d \mathbf{v}_d$$

thì $\mathbf{x}$ được gọi là **tổ hợp tuyến tính** (hay **linear combination**) của các vector $\mathbf{v}_i$, $i = 1, 2, \ldots, d$.
````

Ta thấy rằng vector không $\mathbf{0}$ là tổ hợp tuyến tính của mọi tập các vector $\mathbf{v}_i$ khi tất cả $\alpha_i = 0$.

Bây giờ ta xét tổ hợp tuyến tính

$$\alpha_1 \mathbf{v}_1 + \alpha_2 \mathbf{v}_2 + \ldots + \alpha_d \mathbf{v}_d = \mathbf{0}$$

````{prf:definition} Độc lập tuyến tính
Tập hợp các vector $\mathbf{v}_1$, $\mathbf{v}_2$, ..., $\mathbf{v}_d$ được gọi là **độc lập tuyến tính** (hay **linear independent**) nếu chỉ có duy nhất trường hợp $\alpha_1 = \alpha_2 = \ldots = \alpha_d = 0$ thỏa tổ hợp tuyến tính trên.    
````

````{prf:definition} Phụ thuộc tuyến tính
Tập các vector là **phụ thuộc tuyến tính** (hay **linear dependent**) nếu không độc lập tuyến tính. Nói cách khác tồn tại ít nhất một phần tử $\alpha_i \neq 0$.
````

## Không gian vector

### Không gian vector

Xét tập hợp các vector $\mathcal{V}$ trên trường $\mathbb{F}$.

Ta định nghĩa hai phép tính cộng và nhân trên các vector này.

1. Phép cộng là một ánh xạ $\mathcal{V} \times \mathcal{V} \to \mathcal{V}$ sao cho với mọi $\mathbf{x}, \mathbf{y} \in \mathcal{V}$ thì $\mathbf{x} + \mathbf{y} \in \mathcal{V}$
2. Phân nhân vô hướng là ánh xạ $\mathbb{F} \times \mathcal{V} \to \mathcal{V}$ sao cho với mọi $\alpha \in \mathbb{F}$ và $\mathbf{x} \in \mathcal{V}$ thì $\alpha \mathbf{x} \in \mathcal{V}$

Nói cách khác, phép cộng 2 vector và phép nhân vô hướng 1 số với vector cho kết quả vẫn nằm trong không gian vector đó.

Đồng thời, phép cộng và phép nhân vô hướng phải thỏa mãn các tính chất sau

1. Tính giao hoán với phép cộng: với mọi $\mathbf{x}, \mathbf{y} \in \mathcal{V}$, $\mathbf{x} + \mathbf{y} = \mathbf{y} + \mathbf{x}$
2. Tính kết hợp với phép cộng: với mọi $\mathbf{x}, \mathbf{y}, \mathbf{z} \in \mathcal{V}$, $\mathbf{x} + (\mathbf{y} + \mathbf{z}) = (\mathbf{x} + \mathbf{y}) + \mathbf{z}$
3. Phần tử đơn vị của phép cộng: tồn tại vector không $\mathbf{0} \in \mathcal{V}$ sao cho với mọi $\mathbf{x} \in \mathcal{V}$, $\mathbf{0} + \mathbf{x} = \mathbf{x} + \mathbf{0} = \mathbf{x}$
4. Phần tử đối của phép cộng: với mọi $\mathbf{x} \in \mathcal{V}$, tồn tại phần tử $\mathbf{x'} \in \mathcal{V}$ sao cho $\mathbf{x} + \mathbf{x'} = \mathbf{x} + \mathbf{x'} = \mathbf{0}$
5. Phần tử đơn vị của phép nhân vô hướng: tồn tại phần tử $1_F \in \mathbb{F}$ sao cho với mọi $\mathbf{x} \in \mathcal{V}$ thì $1_F \cdot \mathbf{x} = \mathbf{x}$
6. Tính kết hợp của phép nhân vô hướng: với mọi $\alpha, \beta \in \mathbb{F}$, với mọi $\mathbf{x} \in \mathcal{V}$ thì $\alpha (\beta \mathbf{x}) = (\alpha \beta) \mathbf{x}$
7. Tính phân phối giữa phép cộng và nhân: với mọi $\alpha \in \mathbb{F}$, với mọi $\mathbf{x}, \mathbf{y} \in \mathcal{V}$ thì $\alpha (\mathbf{x} + \mathbf{y}) = \alpha \mathbf{x} + \alpha \mathbf{y}$
8. Tính phân phối giữa phép nhân vô hướng: với mọi $\alpha, \beta \in \mathbb{F}$, với mọi $\mathbf{x} \in \mathcal{V}$ thì $(\alpha + \beta) \mathbf{x} = \alpha \mathbf{x} + \beta \mathbf{x}$

Ta thấy rằng không gian vector ở chương trình phổ thông là không gian vector xác định trên trường $\mathbb{F} = \mathbb{R}$.

Khi đó $\mathcal{V} = \mathbb{R}^n$. Trong chương này sẽ làm việc với không gian vector thực $\mathbb{R}$.

### Cơ sở và số chiều của không gian vector

Nếu trong không gian vector $\mathcal{V}$ tồn tại các vector độc lập tuyến tính $\mathbf{v}_1$, $\mathbf{v}_2$, ..., $\mathbf{v}_d$ mà tất cả các vector trong $\mathcal{V}$ có thể biểu diễn dưới dạng tổ hợp tuyến tính của các vector $\mathbf{v}_i$ trên, thì tập hợp các vector 

$$\{ \mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d \}$$

được gọi là **cơ sở** của không gian vector $\mathcal{V}$.

Khi đó

$$\mathbf{x} = \sum_{i=1}^{d} \alpha_i \mathbf{v}_i \quad \text{với mọi} \ \mathbf{x} \in \mathcal{V}$$

Số lượng phần tử của tập hợp các vector đó (ở đây là $d$) gọi là **số chiều** (hay **dimension**) của không gian vector $\mathcal{V}$. Ta ký hiệu $\text{dim} \mathcal{V} = d$.

Ta còn ký hiệu

$$\mathcal{V} = \text{span} \{\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d\}$$

và nói là không gian vector $\mathcal{V}$ được span (hay được sinh) bởi các vector $\mathbf{v_i}$.

Ta thấy rằng có thể có nhiều cơ sở cho cùng một không gian vector.

````{prf:theorem}
Mọi cơ sở của không gian vector $\mathcal{V}$ đều có số phần tử bằng $\text{dim} \mathcal{V}$.
````

Giả sử ta có $\mathbf{v}_1$, $\mathbf{v}_2$, ..., $\mathbf{v}_d$ là một cơ sở của không gian vector $\mathbb{R}^n$. Khi đó nếu hệ vector $\mathbf{w}_1$, $\mathbf{w}_2$, ..., $\mathbf{w}_d$ cũng là một hệ cơ sở khi và chỉ khi tồn tại ma trận khả nghịch $\mathbf{A}$ sao cho $\mathbf{W} = \mathbf{A} \cdot \mathbf{V}$. Ở đây $\mathbf{W}$ là ma trận với các hàng là các vector $\mathbf{w}_i$. Tương tự $\mathbf{V}$ là ma trận với các hàng là các vector $\mathbf{v}_i$.

```{admonition} **Chứng minh.**
:class: danger, dropdown
Ta viết các vector $\mathbf{v}_i$ dưới dạng $\mathbb{R}^n$.

$$\begin{align*}
    \mathbf{v}_1 & = (v_{11}, v_{12}, \ldots, v_{1n}) \\
    \mathbf{v}_2 & = (v_{21}, v_{22}, \ldots, v_{2n}) \\
    \ldots & = (\ldots, \ldots, \ldots, \ldots) \\
    \mathbf{v}_d & = (v_{d1}, v_{d2}, \ldots, v_{dn})
\end{align*}$$

Tương tự là các vector $\mathbf{w}_i$.

$$\begin{align*}
    \mathbf{w}_1 & = (w_{11}, w_{12}, \ldots, w_{1n}) \\
    \mathbf{w}_2 & = (w_{21}, w_{22}, \ldots, w_{2n}) \\
    \ldots & = (\ldots, \ldots, \ldots, \ldots) \\
    \mathbf{w}_d & = (w_{d1}, w_{d2}, \ldots, w_{dn})
\end{align*}$$

Do $\mathbf{v}_i$ là một cơ sở của $\mathbb{R}^n$, mọi vector trong $\mathbb{R}^n$ được biểu diễn dưới dạng tổ hợp tuyến tính của các $\mathbf{v}_i$.

Khi đó ta viết các $\mathbf{w}_i$ dưới dạng tổ hợp tuyến tính của $\mathbf{v_i}$.

$$\begin{align*}
    \mathbf{w}_1 & = \alpha_{11} \mathbf{v}_1 + \alpha_{12} \mathbf{v}_2 + \ldots + \alpha_{1d} \mathbf{v}_d \\
    \mathbf{w}_2 & = \alpha_{21} \mathbf{v}_1 + \alpha_{22} \mathbf{v}_2 + \ldots + \alpha_{2d} \mathbf{v}_d \\
    \ldots & = \ldots \\
    \mathbf{w}_d & = \alpha_{d1} \mathbf{v}_1 + \alpha_{d2} \mathbf{v}_2 + \ldots + \alpha_{dd} \mathbf{v}_d
\end{align*}$$

Điều này tương đương với 

$$\begin{equation*}
    \begin{pmatrix}
        w_{11} & w_{12} & \ldots & w_{1n} \\
        w_{21} & w_{22} & \ldots & w_{2n} \\
        \ldots & \ldots & \ldots & \ldots \\
        w_{d1} & w_{d2} & \ldots & w_{dn}
    \end{pmatrix}
    = \begin{pmatrix}
        \alpha_{11} & \alpha_{12} & \ldots & \alpha_{1d} \\
        \alpha_{21} & \alpha_{22} & \ldots & \alpha_{2d} \\
        \ldots & \ldots & \ldots & \ldots \\
        \alpha_{d1} & \alpha_{d2} & \ldots & \alpha_{dd}
    \end{pmatrix}
    \times \begin{pmatrix}
        v_{11} & v_{12} & \ldots & v_{1n} \\ 
        v_{21} & v_{22} & \ldots & v_{2n} \\ 
        \ldots & \ldots & \ldots & \ldots \\ 
        v_{d1} & v_{d2} & \ldots & v_{dn}
    \end{pmatrix}
\end{equation*}$$

Nếu $\mathbf{w}_i$ cũng là cơ sở của $\mathcal{V}$, thì các vector $\mathbf{v}_i$ cũng phải biểu diễn được dưới dạng tổ hợp tuyến tính của $\mathbf{w}_i$.
Nói cách khác, ma trận $(\alpha_{ij})$ khả nghịch và ta có điều phải chứng minh.
```

### Không gian vector con

Cho không gian vector $\mathcal{V} \subset \mathbb{R}^n$ với phép cộng hai vector và phép nhân vô hướng. Một tập con $L$ của $\mathcal{V}$ được gọi là không gian vector con nếu:

1. Với mọi $\mathbf{x}$, $\mathbf{y}$ thuộc $L$, $\mathbf{x} + \mathbf{y} \in L$
2. Với mọi $\alpha \in \mathbb{R}$, với mọi $\mathbf{x} \in L$, $\alpha \mathbf{x} \in L$

Nói cách khác, phép cộng và phép nhân vô hướng **đóng** (hay **closure**) trên không gian vector con.

````{prf:remark}
Trên $\mathbb{R}^n$, hệ phương trình tuyến tính thuần nhất có thể sinh ra một không gian vector con của $\mathbb{R}^n$.
````

````{prf:example}
Xét hệ phương trình tuyến tính sau:

$$\begin{equation*}
    \begin{array}{cccccccc}
        x_1 & + & 3x_2 & + & 5x_3 & + & 7x_4 & = 0 \\
        2x_1 & & & + & 4x_3 & + & 2x_4 & = 0 \\
        3x_1 & + & 2x_2 & + & 8x_3 & + & 7x_4 & = 0
    \end{array}
\end{equation*}$$

Biến đổi ma trận

$$\begin{equation*}
    \begin{pmatrix}
        1 & 3 & 5 & 7 \\
        2 & 0 & 4 & 2 \\
        3 & 2 & 8 & 7
    \end{pmatrix} \sim \begin{pmatrix}
        1 & 3 & 5 & 7 \\
        0 & -6 & -6 & -12 \\
        0 & -7 & -7 & -14
    \end{pmatrix} \sim \begin{pmatrix}
        1 & 3 & 5 & 7 \\
        0 & 1 & 1 & 2 \\
        0 & 0 & 0 & 0
    \end{pmatrix}
\end{equation*}$$

Như vậy hệ tương đương với

$$x_1 + 3x_2 + 5x_3 + 7x_4 = 0, \quad x_2 + x_3 + 2x_4 = 0$$

Ta chọn $x_3, x_4 \in \mathbb{R}$ tự do, khi đó $x_1$ và $x_2$ được biểu diễn theo $x_3$ và $x_4$ 

$$\begin{equation*}
    x_1 = -2x_3 - x_4, \quad x_2 = -x_3 - 2x_4
\end{equation*}$$

Mọi vector trong không gian tuyến tính khi đó có dạng

$$\begin{align*}
    (x_1, x_2, x_3, x_4) & = (-2x_3 - x_4, -x_3 - 2x_4, x_3, x_4)
    \\ & = x_3 \cdot (-2, -1, 1, 0) + x_4 \cdot (-1, -2, 0, 1) 
\end{align*}$$

Ở đây ta thấy $x_3, x_4$ nhận giá trị tùy ý trong $\mathbb{R}$, và mọi vector trong không gian nghiệm là tổ hợp tuyến tính của hai vector $(-2, -1, 1, 0)$ và $(-1, -2, 0, 1)$. Suy ra hai vector này là cơ sở của không gian nghiệm, và $\dim \mathcal{V} = 2$.
````

## Không gian Euclide

Trên không gian vector $\mathcal{V}$ chúng ta bổ sung thêm một phép toán là tích vô hướng (dot product, tích chấm) của hai vector.

Giả sử với hai vector $\mathbf{x} = (x_1, x_2, \ldots, x_n)$ và $\mathbf{y} = (y_1, y_2, \ldots, y_n)$. Khi đó tích vô hướng của $\mathbf{x}$ và $\mathbf{y}$ là

$$\begin{equation}
	\mathbf{x} \cdot \mathbf{y} = x_1 y_1 + x_2 y_2 + \ldots + x_n y_n
\end{equation}$$

Một số sách ký hiệu tích vô hướng của hai vector $\mathbf{x}$ và $\mathbf{y}$ là $\langle \mathbf{x}, \mathbf{y} \rangle$. Trong phần này này mình sẽ dùng ký hiệu $\mathbf{x} \cdot \mathbf{y}$ như trên.

Không gian vector có phép toán tích vô hướng được gọi là không gian Euclide. Khi $\mathbf{x} = \mathbf{y}$ thì căn bậc hai của kết quả tích vô hướng được gọi là **chuẩn Euclide** (hay **Euclidean norm**) và được ký hiệu

$$\begin{equation}
	\lVert \mathbf{x} \rVert = \sqrt{\mathbf{x} \cdot \mathbf{x}} = \sqrt{x_1^2 + x_2^2 + \ldots + x_n^2}
\end{equation}$$

Như vậy ta có thể viết $\lVert \mathbf{x} \rVert^2 = \mathbf{x}^2$.

````{prf:theorem} Bất đẳng thức Cauchy-Schwarz
Với hai vector $\mathbf{x}$ và $\mathbf{y}$ bất kì ta luôn có

$$\begin{equation}
    \lVert \mathbf{x} \rVert \cdot \lVert \mathbf{y} \rVert \geqslant \lvert \mathbf{x} \cdot \mathbf{y} \rvert
\end{equation}$$

Nghĩa là tích độ dài của hai vector bất kì trong cùng không gian Euclide lớn hơn hoặc bằng tích vô hướng giữa chúng. Dấu bằng xảy ra khi và chỉ khi $\dfrac{x_1}{y_1} = \dfrac{x_2}{y_2} = \ldots = \dfrac{x_n}{y_n}$. Nói cách khác là hai vector cùng phương.
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
Với mọi số thực $t$, ta luôn có 

$$0 \leqslant \lVert \mathbf{x} - t \mathbf{y} \rVert^2 = \mathbf{x}^2 - 2 t \mathbf{x} \cdot \mathbf{y} + t^2 \mathbf{y}^2 = \lVert \mathbf{x} \rVert^2 - 2 t \mathbf{x} \cdot \mathbf{y} + t^2 \lVert \mathbf{y} \rVert^2$$

Nếu xem biểu thức trên là đa thức bậc 2 theo $t$, để đa thức lớn hơn hoặc bằng 0 với mọi $t \in \mathbb{R}$ thì ta phải có $\Delta' \leqslant 0$ và $\lVert \mathbf{y} \rVert^2 > 0$ (luôn đúng). Ta có

$$\Delta' = (\mathbf{x} \cdot \mathbf{y})^2 - \lVert \mathbf{x} \rVert^2 \cdot \lVert \mathbf{y} \rVert^2 \leqslant 0$$

Tương đương với $\lvert \mathbf{x} \cdot \mathbf{y} \rvert \leqslant \lVert \mathbf{x} \rVert \cdot \lVert \mathbf{y} \rVert$ (điều phải chứng minh).
```

### Hệ cơ sở trực giao

Cho không gian Euclide $\mathcal{V}$ và một cơ sở của nó là $\mathbf{v}_1$, $\mathbf{v}_2$, ..., $\mathbf{v}_d$. Thuật toán trực giao Gram-Schmidt là thuật toán biến đổi cơ sở trên thành một cơ sở mới, trong đó các vector đều trực giao nhau.

````{prf:algorithm} Thuật toán trực giao Gram-Schmidt
**Input:** $\mathbf{v}_1$, ..., $\mathbf{v}_d$ trong $\mathbb{R}^n$

**Output:** $\mathbf{u}_1$, ..., $\mathbf{u}_d$ trong $\mathbb{R}^n$ mà $\mathbf{u}_i \cdot \mathbf{u}_j = 0$ với mọi $i \neq j$

1. $\mathbf{u}_1 \gets \mathbf{v}_1$
2. for $i = 2$ to $d$
    1. $\mathbf{w} = \mathbf{v}_i$
	2. for $j = i-1$ to $1$
		1. $\mu_{i,j} = (\mathbf{v}_i \cdot \mathbf{u}_j) / (\mathbf{u}_i \cdot \mathbf{u}_j)$
		2. $\mathbf{w} \gets \mathbf{w} - \mu_{i, j} \mathbf{u}_j$
    3. $\mathbf{u}_i \gets \mathbf{w}$

3. Trả về cơ sở trực giao $\mathbf{u}_1$, ..., $\mathbf{u}_d$
````

Nói cách khác, với $\mathbf{u}_1 = \mathbf{v}_1$, với mỗi $i = 2, 3, \ldots, d$ ta tính vector $\mathbf{u}_i$ với công thức

$$\begin{equation*}
	\mathbf{u}_i = \mathbf{v}_i - \sum_{j=1}^{i-1} \mu_{i,j} \mathbf{u}_j
\end{equation*}$$

Ở đây $\mu_{i,j} = \dfrac{\mathbf{v}_i \cdot \mathbf{u}_j}{\mathbf{u}_i \cdot \mathbf{u}_j}$ là hệ số trước $\mathbf{u}_j$.

````{prf:example}
Xét cơ sở $\mathbf{v}_1 = (2, -2, 4)$, $\mathbf{v}_2 = (1, -1, 0)$ và $\mathbf{v}_3 = (5, -3, 3)$ của $\mathbb{R}^3$.

Đặt $\mathbf{u}_1 = \mathbf{v}_1 = (2, -2, 4)$.

Ta có $\mu_{2,1} = \dfrac{\mathbf{v}_2 \cdot \mathbf{u}_1}{\mathbf{u}_1 \cdot \mathbf{u}_1} = \dfrac{1 \cdot 2 + (-1) \cdot (-2) + 0 \cdot 4}{2^2 + (-2)^2 + 4^2} = \dfrac{4}{24} = \dfrac{1}{6}$.

Suy ra

$$\mathbf{u}_2 = \mathbf{v_2} - \mu_{2, 1} \mathbf{u}_1 = (1, -1, 0) - \dfrac{1}{6} \cdot (2, -2, 4) = \Bigl(\dfrac{2}{3}, \dfrac{-2}{3}, \dfrac{-2}{3}\Bigr)$$

Tương tự $\mu_{3, 1} = \dfrac{\mathbf{v}_3 \cdot \mathbf{u}_1}{\mathbf{u}_1 \cdot \mathbf{u}_1} = \dfrac{5 \cdot 2 + (-3) \cdot (-2) + 3 \cdot 4}{2^2 + (-2)^2 + 4^2} = \dfrac{28}{24} = \dfrac{7}{6}$.

Tiếp theo $\mu_{3,2} = \dfrac{\mathbf{v}_3 \cdot \mathbf{u}_2}{\mathbf{u}_2 \cdot \mathbf{u}_2} = \dfrac{5 \cdot \dfrac{2}{3} + (-3) \cdot \dfrac{-2}{3} + 3 \cdot \dfrac{-2}{3}}{ \Bigl(\dfrac{2}{3}\Bigr)^2 + \Bigl(\dfrac{-2}{3}\Bigr)^2 + \Bigl(\dfrac{-2}{3}\Bigr)^2 } = \dfrac{5}{2}$.

$$\begin{align*}
    \Rightarrow \quad \mathbf{u}_3 = & \mathbf{v}_3 - \mu_{3,1} \mathbf{u}_1 - \mu_{3,2} \mathbf{u}_2 \\ = & (5, -3, 3) - \dfrac{7}{6} \cdot (2, -2, 4) - \dfrac{5}{2} \cdot \Big(\dfrac{2}{3}, \dfrac{-2}{3}, \dfrac{-2}{3}\Big) \\ = & (1, 1, 0)
\end{align*}$$

Ta có thể kiếm chứng rằng $\mathbf{u}_1 \cdot \mathbf{u}_2 = 2 \cdot \dfrac{2}{3} + (-2) \cdot \dfrac{-2}{3} + 4 \cdot \dfrac{-2}{3} = 0$. Tương tự với $\mathbf{u}_1 \cdot \mathbf{u}_3 = 0$ và $\mathbf{u}_2 \cdot \mathbf{u}_3 = 0$. Thêm nữa các vector này cũng độc lập tuyến tính nên cũng là một hệ cơ sở của $\mathbb{R}^3$.

Như vậy các vector $\mathbf{u}_1$, $\mathbf{u}_2$, $\mathbf{u}_3$ là một cơ sở trực giao của $\mathbb{R}^3$.
````

````{prf:remark}
Cơ sở trực giao cho phép ta tính độ dài của tất cả các vector khác trong không gian vector dễ dàng hơn.
````

Thật vậy, giả sử $\mathbf{u}_1$, $\mathbf{u}_2$, ..., $\mathbf{u}_d$ là các vector trong cơ sở trực giao. Mọi vector $\mathbf{x}$ trong không gian vector đều có dạng

$$\mathbf{x} = \alpha_1 \mathbf{u}_1 + \alpha_2 \mathbf{u}_2 + \ldots + \alpha_d \mathbf{u}_d$$

Khi đó

$$\begin{align*}
    \lVert \mathbf{x} \rVert^2 = \mathbf{x}^2 = (\alpha_1 \mathbf{u}_1 + \alpha_2 \mathbf{u}_2 + \ldots + \alpha_d \mathbf{u}_d)^2 = \sum_{i=1}^d \alpha_i^2 \mathbf{u}_i^2 + 2 \sum_{i \neq j} \mathbf{u}_i \mathbf{u}_j
\end{align*}$$

Do các vector trong cơ sở đều trực giao với nhau nên $\mathbf{u}_i \cdot \mathbf{u}_j = 0$ với $i \neq j$, $1 \leqslant i, j \leqslant d$. Từ đó ta có được

$$\lVert \mathbf{x} \rVert^2 = \sum_{i=1}^d \alpha_i^2 \mathbf{u}_i^2 = \sum_{i=1}^d \alpha_i^2 \lVert \mathbf{u}_i \rVert^2$$

hay

$$\lVert \mathbf{x} \rVert = \sqrt{\alpha_1^2 \mathbf{u}_1^2 + \ldots + \alpha_d^2 \mathbf{u}_d^2}$$

Kết quả rất đơn giản, độ dài của các vector bất kì là căn bậc hai của tổ hợp độ dài các vector trong cơ sở và hệ số tương ứng.

### Chứng minh thuật toán Gram-Schmidt

Cho không gian vector $\mathcal{V}$ với cơ sở là các vector $\mathbf{v}_1$, ..., $\mathbf{v}_d$. Thuật toán Gram-Schmidt biến đổi và cho kết quả là cơ sở mới $\mathbf{u}_1$, ..., $\mathbf{u}_d$ sao cho các vector trong cơ sở mới này trực giao nhau đôi một.

Đặt $\mathbf{u}_1 = \mathbf{v}_1$. 

**Bước 1.** Ta chứng minh với mọi $k \geqslant 2$ thì $\mathbf{u}_k \cdot \mathbf{u}_1 = 0$.

Ta có $\mathbf{u}_2 = \mathbf{v}_1 - \mu_{2, 1} \mathbf{u_1} = \mathbf{v}_2 - \dfrac{\mathbf{v}_2 \cdot \mathbf{u}_1}{\mathbf{u}_1 \cdot \mathbf{u}_1} \cdot \mathbf{u}_1$. 

Suy ra $\mathbf{u}_2 \cdot \mathbf{u}_1 = \mathbf{v}_2 \cdot \mathbf{u}_1 - \dfrac{\mathbf{v}_2 \cdot \mathbf{u}_1}{\mathbf{u}_1 \cdot \mathbf{u}_1} \cdot (\mathbf{u}_1 \cdot \mathbf{u}_1) = \mathbf{v}_2 \cdot \mathbf{u}_1 - \mathbf{v}_2 \cdot \mathbf{u}_1 = 0$.

Như vậy với $k = 2$ thì đẳng thức đúng. Giả sử đẳng thức $\mathbf{u}_k \cdot \mathbf{u}_1 = 0$ đúng tới $k \geqslant 2$. Xét $k+1$ ta có

$$\mathbf{u}_{k+1} = \mathbf{v}_{k+1} - \sum_{j=1}^{k} \mu_{k+1, j} \mathbf{u}_j$$

Suy ra

$$\mathbf{u}_{k+1} \cdot \mathbf{u}_1 = \mathbf{v}_{k+1} \cdot \mathbf{u}_1 - \sum_{j=1}^{k} \dfrac{\mathbf{v}_{k+1} \cdot \mathbf{u}_j}{\mathbf{u}_j \cdot \mathbf{u}_j} \cdot (\mathbf{u}_j \cdot \mathbf{u}_1 )$$

Ta thấy rằng với $j = 2, \ldots, k$ thì $\mathbf{u}_j \cdot \mathbf{u}_1 = 0$ theo giả thiết quy nạp. Như vậy chỉ còn lại $j = 1$ và kết quả là

$$\mathbf{u}_{k+1} \cdot \mathbf{u}_1 = \mathbf{v}_{k+1} \cdot \mathbf{u}_1 - \dfrac{\mathbf{v}_{k+1} \cdot \mathbf{u}_1}{\mathbf{u}_1 \cdot \mathbf{u}_1} \cdot (\mathbf{u}_1 \cdot \mathbf{u}_1) = 0$$

**Bước 2.** Ta chứng minh với mọi $k \geqslant 3$ thì $\mathbf{u}_k \cdot \mathbf{u}_2 = 0$.

Tương tự ta sử dụng quy nạp. Ta có $\mathbf{u}_3 = \mathbf{v}_3 - \mu_{3,2} \mathbf{u}_2 - \mu_{3,1} \mathbf{u}_1$. Suy ra $\mathbf{u}_3 \cdot \mathbf{u}_2 = \mathbf{v}_3 \cdot \mathbf{u}_2 - \mu_{3,2} \mathbf{u}_2 \cdot \mathbf{u}_2 - \mu_{3,1} \cdot \mathbf{u}_1 \cdot \mathbf{u}_2$. Ta đã chứng minh được $\mathbf{u}_2 \cdot \mathbf{u}_1 = 0$. Như vậy kết quả sẽ là

$$\mathbf{u}_3 \cdot \mathbf{u}_2 = \mathbf{v}_3 \cdot \mathbf{u}_2 - \dfrac{\mathbf{v}_3 \cdot \mathbf{u}_2}{\mathbf{u}_2 \cdot \mathbf{u}_2} \cdot (\cdot \mathbf{u}_2 \cdot \mathbf{u}_2) = 0$$

Với giả thiết quy nạp $\mathbf{u}_k \cdot \mathbf{u}_2 = 0$ đúng tới $k \geqslant 3$, ta xét $k+1$. Khi đó

$$\mathbf{u}_{k+1} = \mathbf{v}_{k+1} - \sum_{j=1}^k \mu_{k+1,j} \mathbf{u}_j$$

Suy ra

$$\mathbf{u}_{k+1} \cdot \mathbf{u}_2 = \mathbf{v}_{k+1} \cdot \mathbf{u}_2 - \sum_{j=1}^k \mu_{k+1,j} \mathbf{u}_j \cdot \mathbf{u}_2$$

Theo giả thiết quy nạp thì mọi $j \geqslant 3$ đều cho kết quả $\mathbf{u}_j \cdot \mathbf{u}_2 = 0$, thêm nữa là $\mathbf{u}_1 \cdot \mathbf{u}_2 = 0$ do chứng minh trên. Như vậy trong tổng chỉ còn lại $j=2$ và kết quả sẽ là

$$\mathbf{u}_{k+1} \cdot \mathbf{u}_2 = \mathbf{v}_{k+1} \cdot \mathbf{u}_2 - \dfrac{\mathbf{v}_{k+1} \cdot \mathbf{u}_2}{\mathbf{u}_2 \cdot \mathbf{u}_2} \cdot (\mathbf{u}_2 \cdot \mathbf{u}_2) = 0$$

Từ đây có thể thấy, sử dụng phương pháp quy nạp ta có thể chứng minh được rằng với mỗi số $n \geqslant 2$, thì mọi $k \geqslant n+1$ ta đều có $\mathbf{u}_k \cdot \mathbf{u}_n = 0$. Hay nói cách khác là khi thuật toán tính $\mathbf{u}_k$ thì nó sẽ trực giao với tất cả $\mathbf{u}_1$, $\mathbf{u}_2$, ..., $\mathbf{u}_{k-1}$.

## Trị riêng và vector riêng

### Trị riêng và vector riêng

````{prf:definition} Trị riêng và vector riêng
Xét toán tử tuyến tính được biểu diễn bởi ma trận $\mathbf{A}$. Khi đó vector $\mathbf{v}$ khác không được gọi là **vector riêng** (hay **eigenvector**) của ma trận nếu tồn tại phần tử $\lambda$ sao cho

$$\begin{equation*}
    \mathbf{A} \mathbf{v} = \lambda \mathbf{v}
\end{equation*}$$

Giá trị $\lambda$ khi đó gọi là **trị riêng** (hay **eigenvalue**) tương ứng với vector riêng $\mathbf{v}$.
````

Chuyển vế đẳng thức trên ta có $(\mathbf{A} - \lambda \mathbf{I}) \cdot \mathbf{v} = \mathbf{0}$. Ở đây $\mathbf{I}$ là ma trận cùng cỡ với $\mathbf{A}$ và có các phần tử ở hàng $i$ và cột $i$ bằng 1.

Như vậy, để phương trình có nghiệm khác không thì ma trận $\mathbf{A} - \lambda \mathbf{I}$ suy biến, hay $\det (\mathbf{A} - \lambda \mathbf{I}) = 0$.

Mỗi nghiệm $\lambda$ của phương trình $\det (\mathbf{A} - \lambda \mathbf{I}) = 0$ là một trị riêng. Với mỗi trị riêng $\lambda$ ta tìm được một vector riêng $\mathbf{v}$.

