## Đạo hàm một số hàm nhiều biến

### Hàm số cho giá trị là số vô hướng
	
Giả sử ta có vector hàng $\bm{x} = (x_1, \ldots, x_n)$ và hàm số $f$ có biến là vector $\bm{x}$. Nói cách khác là $f: \mathbb{R}^n \to \mathbb{R}$, $f(\bm{x}) = f(x_1, \ldots, x_n)$.

Khi đó đạo hàm riêng của hàm $f$ theo vector $\bm{x}$ cũng là một vector (nếu $\bm{x}$ là vector hàng thì đạo hàm riêng cũng là vector hàng và ngược lại) và được ký hiệu

$$\begin{equation*}
    \nabla f(\bm{x}) = \begin{pmatrix}
        \dfrac{\partial f}{\partial x_1} & \cdots & \dfrac{\partial f}{\partial x_n}
    \end{pmatrix}
\end{equation*}$$

Ví dụ, đối với hàm tuyến tính

$$f(\bm{x}) = a_1 x_1 + \ldots + a_n x_n = \bm{a} \cdot \bm{x}^\top$$

thì ta thấy rằng $\dfrac{\partial f}{\partial x_i} = a_i$. Khi đó 

$$\nabla f (\bm{x}) = \begin{pmatrix}
    \dfrac{\partial f}{\partial x_1} & \cdots & \dfrac{\partial f}{\partial x_n}
\end{pmatrix} = (a_1, \ldots, a_n) = \bm{a}$$

Ta thấy rằng $f(\bm{x}) = \bm{a} \cdot \bm{x}^\top = \bm{x} \cdot \bm{a}^\top$. Do đó

$$\nabla (\bm{a} \cdot \bm{x}^\top) = \nabla (\bm{x} \cdot \bm{a}^\top) = \bm{a}$$

Đạo hàm riêng cấp hai được cho bởi ma trận được gọi là ma trận Hessian.

$$\begin{equation*}
    \nabla^2 f(\bm{x}) = \begin{pmatrix}
        \dfrac{\partial^2 f}{\partial x_1^2} & \dfrac{\partial^2 f}{\partial x_1 x_2} & \cdots & \dfrac{\partial^2 f}{\partial x_1 x_n} \\ \dfrac{\partial^2 f}{\partial x_2 x_1} & \dfrac{\partial^2 f}{\partial x_2^2} & \cdots & \dfrac{\partial^2 f}{\partial x_2 x_n} \\ \cdots & \cdots & \ddots & \cdots \\ \dfrac{\partial^2 f}{\partial x_n x_1} & \dfrac{\partial^2 f}{\partial x_n x_2} & \cdots & \dfrac{\partial^2 f}{\partial x_n^2}
    \end{pmatrix}
\end{equation*}$$

Theo tính chất của đạo hàm riêng cấp hai có thể thấy ma trận trên là ma trận đối xứng.

Nếu đầu vào là một ma trận, hay $f: \mathbb{R}^{n \times m} \to \mathbb{R}$, $f(\bm{X})$ thì ta làm tương tự

Giả sử

$$\bm{X} = \begin{pmatrix}
    x_{11} & x_{12} & \cdots & x_{1m} \\ x_{21} & x_{22} & \cdots & x_{2m} \\ \cdots & \cdots & \ddots & \cdots \\ x_{n1} & x_{n2} & \cdots & x_{nm}
\end{pmatrix}$$

Khi đó đạo hàm của hàm $f$ theo ma trận $\bm{X}$ là

$$\begin{equation*}
    \nabla f(\bm{X}) = \begin{pmatrix}
        \dfrac{\partial f}{\partial x_{11}} & \dfrac{\partial f}{\partial x_{12}} & \cdots & \dfrac{\partial f}{\partial x_{1m}} \\ \dfrac{\partial f}{\partial x_{21}} & \dfrac{\partial f}{\partial x_{22}} & \cdots & \dfrac{\partial f}{\partial x_{2m}} \\ \cdots & \cdots & \ddots & \cdots \\ \dfrac{\partial f}{\partial x_{n1}} & \dfrac{\partial f}{\partial x_{n2}} & \cdots & \dfrac{\partial f}{\partial x_{nm}}
    \end{pmatrix}
\end{equation*}$$

Như vậy đạo hàm theo ma trận cũng là ma trận cùng cỡ với ma trận đầu vào.

### Hàm số cho giá trị là vector

Xét hàm vector

$$F(\bm{x}) = (f_1(\bm{x}), f_2(\bm{x}), \ldots, f_m(\bm{x}))$$

với $\bm{x} = (x_1, x_2, \ldots, x_n) \in \mathbb{R}^n$ và các hàm $f_i (\bm{x})$ là hàm từ $\mathbb{R}^n$ tới $\mathbb{R}$. Khi đó hàm vector $F$ là hàm từ $\mathbb{R}^n$ tới $\mathbb{R}^m$.

Nếu $f_i$ là các hàm tuyến tính như trên thì hàm $F$ là một ánh xạ tuyến tính, hay tương đương với phép nhân ma trận $F(\bm{x}) = \bm{x} \cdot \bm{A}$. Ở đây $\bm{x}$ là vector hàng, còn $\bm{A}$ là ma trận $n \times m$.

$$\bm{A} = \begin{pmatrix}
    a_{11} & a_{21} & \cdots & a_{m1} \\ a_{12} & a_{22} & \cdots & a_{m2} \\ \cdots & \cdots & \ddots & \cdots \\ a_{1n} & a_{2n} & \cdots & a_{mn}
\end{pmatrix}$$

Ở đây, $f(\bm{x}) = f_i(x_1, x_2, \ldots, x_n) = a_{i1} x_1 + a_{i2} x_2 + \ldots + a_{in} x_n$. Nếu đặt $\bm{a}_i = (a_{i1}, a_{i2}, \ldots, a_{in})$ thì ma trận $\bm{A}$ có các cột là $\bm{a}_i^\top$. Nói cách khác

$$\bm{A} = \begin{pmatrix}
    \bm{a}_1^\top & \bm{a}_2^\top & \cdots & \bm{a}_m^\top
\end{pmatrix}$$

Nếu ta xét từng cột của ma trận $\bm{A}$ thì hoàn toàn giống trường hợp trên. Giả sử với cột đầu tiên (ứng với $f_1$) ta có

$$f_1 (\bm{x}) = \begin{pmatrix}
    x_1 & x_2 & \cdots & x_n
\end{pmatrix} \cdot \begin{pmatrix}
    a_{11} \\ a_{12} \\ \vdots \\ a_{1n}\end{pmatrix} = \bm{x} \cdot \bm{a}_1^\top$$

Đạo hàm của $f_1$ theo vector $\bm{x}$ là

$$\nabla f_1 (\bm{x}) = \begin{pmatrix}
    a_{11} & a_{12} & \cdots & a_{1n} 
\end{pmatrix} = \bm{a_1}$$

Xếp các hàm $f_i$ từ trên xuống dưới, ta có được đạo hàm của hàm $F$ theo vector $x$ là 

$$\begin{equation*}
    \nabla F(\bm{x}) = \begin{pmatrix}
        \nabla f_1 (\bm{x}) \\ \nabla f_2 (\bm{x}) \\ \vdots \\ \nabla f_m(\bm{x})
    \end{pmatrix}  = \begin{pmatrix}
    \bm{a}_1 \\ \bm{a}_2 \\ \vdots \\ \bm{a}_m
    \end{pmatrix} = \bm{A}^\top
\end{equation*}$$
