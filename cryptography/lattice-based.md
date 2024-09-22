# Lattice-based cryptography

```{contents}
:depth: 2
```

## Introduction

**Ký hiệu**. Vector hàng được ký hiệu bởi chữ thường in đậm, ví dụ $\mathbf{x}, \mathbf{y}, \mathbf{v}$. Ma trận được ký hiệu bởi chữ hoa in đậm, ví dụ $\mathbf{A}, \mathbf{B}$.

````{prf:defintion} Lattice
Xét tập hợp các vector độc lập tuyến tính $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d$ trên $\mathbb{R}^n$. Ta nói **lattice** (hay **lưới**) $\mathcal{L} \subset \mathbb{R}^n$ được sinh bởi các vector $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d$ nếu

$$\mathcal{L} = \{ a_1 \mathbf{v}_1 + a_2 \mathbf{v}_2 + \ldots + a_d \mathbf{v}_d : a_i \in \mathbb{Z} \}$$
````

Nói cách khác, lattice là không gian vector được sinh bởi tổ hợp tuyến tính với hệ số nguyên.

Tập các vector $\{ \mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d \}$ được gọi là **tập sinh** hay **cơ sở** (basis, базис) của lattice $\mathcal{L}$.

Số lượng vector trong cơ sở được gọi là **số chiều** của lattice và kí hiệu là $d = \dim(\mathcal{L})$.

Lattice được gọi là **full-rank** nếu $\dim(\mathcal{L}) = n$.

Xét ma trận $\mathbf{V}$ có các hàng là các vector $\mathbf{v}_1, \ldots, \mathbf{v}_d$, nghĩa là $\mathbf{V} \in \mathbb{R}^{d \times n}$.

````{prf:defintion} Định thức của lattice
**Định thức của lattice** $\mathcal{L}$ được xác định bởi công thức $\displaystyle{\det(\mathcal{L}) = \sqrt{\lvert \det\left(\mathbf{V} \mathbf{V}^\top \right)\rvert}}$.
````

Nếu lattice full-rank thì $\det(\mathcal{L}) = \det(\mathbf{V})$.

````{prf:remark}
Cơ sở của một lưới không là duy nhất nhưng số lượng vector trong mỗi cơ sở là như nhau và bằng số chiều của lattice.
````

Nếu $\mathbf{V}$ và $\mathbf{W}$ là hai ma trận cơ sở của cùng lattice $\mathcal{L}$ thì tồn tại ma trận $\mathbf{A}$ với hệ số nguyên (tức $\mathbf{A} \in \mathbb{Z}^{d \times d}$) có định thức bằng $1$ sao cho $\mathbf{W} = \mathbf{A} \cdot \mathbf{V}$. Chúng ta có thể dễ dàng chứng minh điều này khi biểu diễn các vector trong $\mathbf{W}$ thành tổ hợp tuyến tính các vector trong $\mathbf{V}$.

Giả sử $\{ \mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d \}$ là một cơ sở của $\mathcal{L}$. Tương tự, $\{ \mathbf{w}_1, \mathbf{w}_2, \ldots, \mathbf{w}_d \}$ là một cơ sở khác của $\mathcal{L}$.

Ta có thể viết mỗi $\mathbf{w}_i$ là tổ hợp tuyến tính của các vector $\mathbf{v}$ như sau

$$\begin{align*}
	\mathbf{w}_1 & = a_{11} \mathbf{v}_1 + a_{12} \mathbf{v}_2 + \ldots + a_{1d} \mathbf{v}_d \\
	\mathbf{w}_2 & = a_{21} \mathbf{v}_1 + a_{22} \mathbf{v}_2 + \ldots + a_{2d} \mathbf{v}_d \\
	\vdots & \\
	\mathbf{w}_d & = a_{d1} \mathbf{v}_1 + a_{d2} \mathbf{v}_2 + \ldots + a_{dd} \mathbf{v}_d
\end{align*}$$

Khi đó, nếu viết các vector $\mathbf{w}_i$ thành hàng của ma trận $\mathbf{W}$ và $\mathbf{v}_j$ thành hàng của ma trận $\mathbf{V}$ thì biểu diễn trên tương đương với:

$$\begin{equation*}
	\mathbf{W} = \begin{pmatrix}
		a_{11} & a_{12} & \cdots & a_{1d} \\
		a_{21} & a_{22} & \cdots & a_{2d} \\
		\vdots & \vdots & \ddots & \vdots \\
		a_{d1} & a_{d2} & \cdots & a_{dd}
	\end{pmatrix} \cdot \mathbf{V}
\end{equation*}$$

Đặt

$$\begin{equation*}
	\mathbf{A} = \begin{pmatrix}
		a_{11} & a_{12} & \cdots & a_{1d} \\
		a_{21} & a_{22} & \cdots & a_{2d} \\
		\vdots & \vdots & \ddots & \vdots \\
		a_{d1} & a_{d2} & \cdots & a_{dd}
	\end{pmatrix}
\end{equation*}$$

Do $\mathbf{W}$ và $\mathbf{V}$ là các cơ sở của $\mathcal{L}$ nên nếu các vector $\mathbf{w}_i$ có thể biểu diễn qua các vector $\mathbf{v}_j$ thì ngược lại, các vector $\mathbf{v}_j$ cũng có thể được biểu diễn qua các vector $\mathbf{w}_i$. Suy ra ma trận $\mathbf{A}$ là ma trận khả nghịch. Do $a_{ij} \in \mathbb{Z}$ theo định nghĩa lattice, $\det(\mathbf{A}) \in \mathbb{Z}$.

Hơn nữa, vì:

$$\begin{equation*}
	I = \mathbf{A} \cdot \mathbf{A}^{-1} \Rightarrow 1 = \det (\mathbf{A}) \cdot \det (\mathbf{A}^{-1})
\end{equation*}$$

nên $\det(\mathbf{A}) = \pm 1$.

Mỗi lattice $\mathcal{L}$ có một lattice đối ngẫu (dual lattice), kí hiệu là

$$\mathcal{L}^* = \{ \mathbf{w} \in \mathbb{R}^n : \langle \mathbf{w}, \mathbf{x} \rangle \in \mathbb{Z} \ \text{với mọi} \ \mathbf{x} \in \mathcal{L} \}$$

````{prf:defintion} Fundamental domain
Cho lattice $\mathcal{L}$ có số chiều là $d$ với cơ sở gồm các vector $\{ \mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_d \}$. Ta gọi **fundamental domain** (hay **fundamental parallelepiped**) của $\mathcal{L}$ ứng với cơ sở trên là tập

$$\begin{equation}
    \mathcal{F} (\mathbf{v}_1, \ldots, \mathbf{v}_d) = \{ t_1 \mathbf{v}_1 + \ldots + t_d \mathbf{v}_d : 0 \leqslant t_i < 1 \}
\end{equation}$$
````

Trong mặt phẳng $Oxy$ với hai vector $\mathbf{u}$ và $\mathbf{v}$ không cùng phương thì fundamental domain là hình bình hành tạo bởi hai vector đó.

````{prf:remark}
Gọi $\mathcal{L} \subset \mathbb{R}^n$ là lattice với số chiều là $n$ và gọi $\mathcal{F}$ là fundamental domain của $\mathcal{L}$. Khi đó mọi vetor $\mathbf{w} \in \mathbb{R}^n$ đều có thể viết dưới dạng
	
$$\mathbf{w} = \mathbf{t} + \mathbf{v}$$

với $\mathbf{t}$ duy nhất thuộc $\mathcal{F}$ và $\mathbf{v}$ duy nhất thuộc $\mathcal{L}$.
````	

Một cách tương đương, hợp của các fundamental domains

$$\begin{equation*}
    \mathcal{F} + \mathbf{v} = \{ \mathbf{t} + \mathbf{v} : \mathbf{t} \in \mathcal{F} \}
\end{equation*}$$

với $\mathbf{v}$ là các vector trong $\mathcal{L}$, sẽ cover hết $\mathbb{R}^n$.

````{admonition} **Chứng minh.**
:class: danger, dropdown

Để chứng minh nhận xét trên, giả sử $\{ \mathbf{v}_i : 1 \leqslant i \leqslant n \}$ là cơ sở của $\mathcal{L}$. Khi đó các $\mathbf{v}_i$ độc lập tuyến tính nên cũng là cơ sở của $\mathbb{R}^n$.
	
Ta viết các vector $\mathbf{w} \in \mathbb{R}^n$ dưới dạng tổ hợp tuyến tính của $\mathbf{v}_i$ và tách hệ số trước mỗi vector thành phần nguyên và phần lẻ. Phần nguyên cho vector trong $\mathcal{L}$ và phần lẻ cho vector trong $\mathcal{F}$.
	
Để chứng minh tính duy nhất của tổ hợp, xét hai cách biểu diễn khác nhau của $\mathbf{w}$ và chứng minh hai cách đó là một.
````

````{prf:theorem} Bất đẳng thức Hadamard
Cho lattice $\mathcal{L}$, lấy cơ sở bất kỳ của $\mathcal{L}$ là các vector $\mathbf{v}_1$, ..., $\mathbf{v}_n$ và gọi $\mathcal{F}$ là fundamental domain cho $\mathcal{L}$. Khi đó

$$\begin{equation}
    \det L = \text{Vol} (\mathcal{F}) \leqslant \lVert \mathbf{v}_1 \rVert \cdot \lVert \mathbf{v}_2 \rVert \cdots \lVert \mathbf{v}_n \rVert
\end{equation}$$
````

Cơ sở càng gần với trực giao thì bất đẳng thức Hadamard trên càng trở thành đẳng thức.

````{prf:definition} Đa thức cyclotomic
Với mỗi số nguyên dương $N$, đa thức cyclotomic thứ $N$ là đa thức tối giản (bất khả quy) $\Phi_N$ duy nhất trong $\mathbb{Z}[x]$ mà chia hết $x^N - 1$ nhưng không chia hết $x^k - 1$ với $k < N$ bất kì.
````

Ví dụ, $x^3 - 1 = (x - 1)(x^2 + x + 1)$ thì ta có $\Phi_3 = x^2 + x + 1$ vì $(x^2 - 1) \not\vert (x^2 + x + 1)$ và $(x - 1) \not\vert (x^2 + x + 1)$.

````{prf:remark}
Nếu $d$ là số nguyên tố thì $\Phi_d = 1 + x + x^2 + \ldots + x^{d-1}$.
````

````{prf:remark}
Các đa thức tối giản không chỉ đối với $\mathbb{Z}$ mà còn đối với $\mathbb{Q}$. Ta cũng có thể chứng minh được rằng:

$$x^N - 1 = \prod_{d \mid N} \Phi_d(x)$$
````

````{prf:definition}
Với $i = 1, \ldots, n$, định nghĩa $\lambda_i(\mathcal{L})$ là $\lambda$ nhỏ nhất sao cho $\mathcal{L}$ chứa ít nhất $i$ vector độc lập của chuẩn Euclid (Euclidean norm) tại hầu hết $\lambda$. Cụ thể $\lambda_1(\mathcal{L})$ là độ dài vector khác không ngắn nhất trong $\mathcal{L}$.
````

## Các bài toán khó

```{admonition} **Bài toán 1.** (Bài toán nhóm con ẩn, Hidden Group Problem - HGP).
Cho một nhóm $G$ và một hàm $f$ trên $G$ là hằng số và phân biệt trên các coset của nhóm con $H$ nào đó chưa biết của $G$. Hãy tìm một tập các phần tử sinh của $H$.
```

```{admonition} **Bài toán 2.** (Bài toán vector ngắn nhất, Shortest Vector Problem - SVP)
Cho một cơ sở tùy ý $\mathbf{V}$ của lattice $\mathcal{L}$. Hãy tìm một vector $\mathbf{x} \in \mathcal{L}$ khác không với $\lVert \mathbf{x} \rVert \leqslant \gamma(m) \cdot \lambda_1(\mathcal{L})$.
```

```{admonition} **Bài toán 3.** (Bài toán Learning With Error, LWE Problem)
Cho $n, m, q > 0$ là các số nguyên và $\chi$ là một phân bố trên $\mathbb{Z}$. Với $\mathbf{s} \xleftarrow{\chi} \mathbb{Z}_n$, định nghĩa $\mathcal{D}_{\mathbf{s}, \chi}$ là phân bố lấy các mẫu $\mathbf{a} \xleftarrow{\$} \mathbb{Z}_q^n$ và $e \xleftarrow{\chi} \mathbb{Z}$. Kết quả trả về $(\mathbf{a}, \langle \mathbf{a}, \mathbf{s} \rangle + e) \in \mathbb{Z}_q^n \times \mathbb{Z}_q$.

1. Với $n, p \geqslant 2$ và $m$ mẫu độc lập từ phân bố $\mathcal{D}_{\mathbf{s}, \chi}$, bài toán LWE tìm kiếm là tìm $\mathbf{s}$ (search LWE problem).

2. Với $n, q \geqslant 2$ và $m$ mẫu độc lập $(\mathbf{a}_i, b_i)$, bài toán LWE quyết định (decisional LWE problem) là phân biệt với $i = 1, \ldots, m$ thì $(\mathbf{a}_i, b_i)$ thuộc $\mathbb{Z}_q^n \times \mathbb{Z}_q$ hay thuộc $\mathcal{D}_{\mathbf{s}, \chi}$. Nói cách khác là được lấy mẫu ngẫu nhiên theo $\mathbb{Z}_q^n \times \mathbb{Z}_q$ hay theo phân bố $\mathcal{D}$.
```

Thông thường chúng ta coi vector $\mathbf{s}$ là secret và $e$ là lỗi (error) của LWE.

Chúng ta nói rằng bài toán LWE quyết định $\text{LWE}_{n, m, q, \chi}$ là $(t, \varepsilon)$-hard nếu đối với bất kì thuật toán $\mathcal{A}$ nào chạy trong thời gian $t$, nó đảm bảo rằng:

$$\left| \mathrm{Pr}\left[ \mathcal{A}^{\mathcal{D}_{\mathbf{s}, \chi}}(\cdot) = 1 \right] - \mathrm{Pr} \left[ \mathcal{A}^{\mathcal{U}(\mathbb{Z}_q^n \times \mathbb{Z}_q)} (\cdot) = 1 \right] \right| \leqslant \varepsilon$$

```{admonition} **Bài toán 4.** (Bài toán Ring-LWE, R-LWE)
Cho $n, q > 0$ là các số nguyên và $\chi$ là phân bố trên $\mathcal{R}$. Với $s \xleftarrow{\$} \mathcal{R}$, định nghĩa $\mathcal{D}_{s, \chi}$ là phân bố lấy các mẫu $a \xleftarrow{\$} \mathcal{R}_q$ và $e \xleftarrow{\chi} \mathcal{R}$. Kết quả trả về $(a, a s + e) \in \mathcal{R}_q \times \mathcal{R}_q$.

Tương tự:

1. Bài toán R-LWE tìm kiếm (search ring-LWE problem) là tìm $s$.
2. Bài toán R-LWE quyết định (decisional ring-LWE problem) là phân biệt $(a_i, b_i) \xleftarrow{\$} \mathcal{R}_q \times \mathcal{R}_q$ hay $(a_i, b_i) \gets \mathcal{D}_{s, \chi}$.
```

### Short vectors trong lattice

Các bài toán liên quan tới lattice mà chúng ta cần quan tâm để xây dựng các thuật toán mã hóa lattice-based.

1. **Shortest Vector Problem** (hay **SVP**): Tìm vector khác không có độ dài ngắn nhất trong lattice $\mathcal{L}$, nghĩa là tìm vector $\mathbf{v} \in L$ mà $\lVert v \rVert$ nhỏ nhất;
2. **Closest Vector Problem** (hay **CVP**): Cho trước vector $\mathbf{w} \in \mathbb{R}^n$ mà không nằm trong $\mathcal{L}$, tìm vector $\mathbf{v} \in L$ gần với $\mathbf{w}$ nhất, nghĩa là tìm $\mathbf{v} \in L$ sao cho $\lVert \mathbf{w} - \mathbf{v} \rVert$ nhỏ nhất.

### Thuật toán Babai

Thuật toán này giúp tìm một cơ sở "đủ tốt" để giải **apprCVP**.

````{prf:theorem} Thuật toán Babai tìm Closest Vertex
Gọi $\mathcal{L} \subset \mathbb{R}^n$ là lattice với cơ sở là $\mathbf{v}_1$, $\mathbf{v}_2$, ..., $\mathbf{v}_n$ và gọi $\mathbf{w} \in \mathbb{R}^n$ là vector bất kỳ. 
	
Nếu các vector trong cơ sở trực giao nhau thì thuật toán Babai sẽ giải được **CVP**.
	
Nếu các vector trong cơ sở gần như trực giao thì thuật toán Babai sẽ giải được **apprCVP**.
	
Ngược lại, nếu các vector trong cơ sở không trực giao (nhiều) thì kết quả thuật toán trả về sẽ xa hơn vector gần với $\mathbf{w}$.
````

````{prf:algorithm} Babai's Closest Vertex Algorithm
1. Biểu diễn $\mathbf{w} = t_1 \mathbf{v}_1 + t_2 \mathbf{v}_2 + \ldots + t_n \mathbf{v}_n$ với $t_1, \ldots, t_n \in \mathbb{R}$.
2. Đặt $a_i = \lfloor t_i \rceil$ với $i = 1, \ldots, n$.
3. Trả về vector $\mathbf{v} = a_1 \mathbf{v}_1 + a_2 \mathbf{v}_2 + \ldots + a_n \mathbf{v}_n$.
````

Mình có thể thấy rằng thuật toán Babai làm tròn hệ số để đưa trả về vector gần với $\mathbf{w}$.

### Lattice reduction

Mục tiêu của việc giải các bài toán **SVP** hay **CVP** (hay các biến thể của chúng) là tìm vector ngắn trong lattice.

Đối với lattice 2 chiều chúng ta có thuật toán Gauss reduction rất hữu dụng.

### Gaussian lattice reduction

Giả sử ta có $\mathcal{L} \subset \mathbb{R}^2$ là lattice 2 chiều với cơ sở là $\mathbf{v}_1$ và $\mathbf{v}_2$.

Ta có thể đổi chỗ $\mathbf{v}_1$ và $\mathbf{v}_2$ nếu cần thiết để luôn đảm bảo $\lVert \mathbf{v}_1 \rVert < \lVert \mathbf{v}_2 \rVert$.

Để làm nhỏ $\mathbf{v}_2$ ta có thể trừ đi một bội số của $\mathbf{v}_1$. Nếu ta sử dụng cách giống như thuật toán trực giao Gram-Schmidt thì

$$\mathbf{v}_2^* = \mathbf{v}_2 - \dfrac{\mathbf{v}_1 \cdot \mathbf{v}_2}{\lVert \mathbf{v}_1 \rVert^2} \mathbf{v}_1$$

Khi đó $\mathbf{v}_2^*$ sẽ trực giao với $\mathbf{v}_1$. Tuy nhiên vector này không nằm trong $\mathcal{L}$ vì hệ số $\dfrac{\mathbf{v}_1 \cdot \mathbf{v}_2}{\lVert \mathbf{v}_1 \rVert^2}$ có thể không phải số nguyên. Để khắc phục ta chỉ việc lấy phần nguyên của hệ số này. Nghĩa là ta thay $\mathbf{v}_2$ bằng vector

$$\mathbf{v}_2 - m \mathbf{v}_1 \quad \text{với}\ m = \left\lfloor \dfrac{\mathbf{v}_1 \cdot \mathbf{v}_2}{\lVert \mathbf{v}_1 \rVert^2} \right\rceil$$

Nếu $\mathbf{v}_2$ vẫn lớn hơn $\mathbf{v}_1$ thì ta dừng thuật toán. Ngược lại ta đảo vị trí $\mathbf{v}_1$ và $\mathbf{v}_2$ rồi lặp lại bước trên. Thuật toán như sau

````{prf:theorem} Gaussian lattice reduction

**Input::** Lattice 2 chiều $\mathcal{L} \subset \mathbb{R}^2$ với cơ sở $\mathbf{v}_1$ và $\mathbf{v}_2$

**Output:** Cơ sở mới $\mathbf{v}_1^*$ và $\mathbf{v}_2^*$ gần như trực giao nhau

1. Nếu $\lVert \mathbf{v}_2 \rVert < \lVert \mathbf{v}_1 \rVert$ thì ta đổi chỗ $\mathbf{v}_1$ và $\mathbf{v}_2$.

2. Tính $m = \left\lfloor \mathbf{v}_1 \cdot \mathbf{v}_2 / \lVert \mathbf{v}_1 \rVert^2 \right\rceil$.

3. Nếu $m = 0$ thì trả về cơ sở gồm $\mathbf{v}_1$ và $\mathbf{v}_2$.

4. Thay $\mathbf{v}_2$ bởi $\mathbf{v}_2 - m \mathbf{v}_1$.
````

## Heuristic

Hai phương pháp heuristic thường được dùng là Gaussian Heuristic (GH) và Geometric Series Assumption (GSA).

GH la một ước lượng của $\lambda_1(\mathcal{L})$ - mật độ của các điểm là $1 / \det(\mathcal{L})$, vì vậy trong một quả cầu có bán kính $r$ thì ta mong đợi sẽ có $v_n \cdot r^n / \det(\mathcal{L})$ điểm trong lattice, trong đó $v_n$ là thể tích của quả cầu đơn vị $n$ chiều.

Cụ thể, điều này đưa ra ước lượng cho $\lambda_1$ thông qua $v_n \cdot \lambda_1^n / \det(\mathcal{L}) \approx 1$, nghĩa là $\lambda_1 = (\det(\mathcal{L}) / v_1)^{1/n}$.

Vì thể tích quả cầu đơn vị là:

$$v_n \approx \dfrac{1}{\sqrt{n \pi}} \left( \dfrac{2 \pi e}{n} \right)^{n/2}$$

GH suy ra:

$$\lambda_1 \approx \det(\mathcal{L})^{1/n} \sqrt{\dfrac{n}{2 \pi e}}$$

## Các thuật toán lattice-based

### Congruential public key cryptosystem

Thuật toán này có thể xem chi trong {cite}`Hoffstein2014`.

#### Tạo khóa

Trong thuật toán này, ta chọn số nguyên tố $q$ làm public parameter.

Sau đó chọn hai số $f$ và $g$ làm private key. Hai số này phải thỏa mãn các điều kiện

$$f < \sqrt{q/2}, \quad \sqrt{q/4} < g < \sqrt{q/2}, \quad \gcd(f, qg) = 1$$

Tính $h = f^{-1} g \pmod q$. Khi đó public key là $h$.

#### Encryption

Để encrypt message $m$ với số random $r$ thỏa mãn 
 
$$0 < m < \sqrt{q/4}, \quad 0 < r < \sqrt{q/2}$$

Ta tính $e = rh + m \pmod q$ là ciphertext với $0 < e < q$.

#### Decryption

Để decrypt ciphertext $e$ ta tính

$$a = fe \pmod q, \quad b = f^{-1} a \pmod g$$

Lưu ý $f^{-1}$ là nghịch đảo modulo $g$. Khi đó $b \equiv m$ là message ban đầu.

````{admonition} **Chứng minh.**
:class: danger, dropdown
Để chứng minh rằng số $b$ sau khi tính toán bằng chính xác $m$ ban đầu ta cần xem xét điều kiện của private key và public key.
	
Đầu tiên ta có 

$$a \equiv fe \equiv f(rh + m) = f(r f^{-1} g + m) = rg + fm \pmod q$$
	
Từ điều kiện của $f$, $g$, $r$ và $m$ ta có

$$rg + fm < \sqrt{\dfrac{q}{2}} \cdot \sqrt{\dfrac{q}{2}} + \sqrt{\dfrac{q}{2}} \cdot \sqrt{\dfrac{q}{4}} < q$$
	
Nói cách khác $rg + fm$ giữ nguyên giá trị trong phép modulo $q$, hay $a \equiv rg + fm$.
	
Suy ra $b = f^{-1} a = f^{-1} (rg + fm) = m \pmod g$ (giá trị $a$ không thay đổi khi chuyển từ modulo $q$ sang modulo $g$). Do $0 < m < \sqrt{q/4}$ và $\sqrt{q/4} < g < \sqrt{q/2}$ nên $m < g$. Nói cách khác $b$ bằng đúng $m$ ban đầu.
````

Để tấn công hệ mật mã này ta xây dựng lattice. Để ý rằng $h = f^{-1} g \pmod q$, hay $fh + kq = g$ với $k \in \mathbb{Z}$.

Ta thấy rằng $f \cdot (h, 1) + k \cdot (q, 0) = (g, f)$. Như vậy lattice gồm hai vector $(h, 1)$ và $(q, 0)$. Thuật toán tối giản Gauss sẽ hoạt động trong trường hợp này (số chiều bằng 2).

### NTRU-HRSS

Hệ mật mã NTRU-HRSS được nộp vòng 1 của dự án NIST PQC. Ở vòng 2, NTRU-HRSS hợp nhất với NTRUEncrypt trở thành NTRU.

#### Các tham số cho NTRU

NTRU hoạt động trên các vành thương (quotient ring) là $\mathbb{Z}[x] / (p, x^n - 1)$ và $\mathbb{Z}[x] / (q, x^n - 1)$. Trong đó $p$, $q$ và $n$ là các số nguyên tố khác nhau.

Ta có thể kí hiệu hai vành trên là $\mathcal{R}_p$ và $\mathcal{R}_q$ để đa thức bất khả quy $x^n - 1$ là ẩn (implicit).

Đối với NTRU-HRSS cần thêm các vành con của $\mathcal{R}_p$ và $\mathcal{R}_q$ mà xác định bằng việc dùng đa thức cyclotomic. Ký hiệu đa thức cyclotomic thứ $d$ là $\Phi_d$. Nhận xét bên trên: $\Phi_1 = x - 1$ và nếu $d$ là số nguyên tố thì $\Phi_d = 1 + x + \ldots + x^{d-1}$.

Đặt $\mathcal{S}_p = \mathbb{Z}[x] / (p, \Phi_n)$ và $\mathcal{S}_q = \mathbb{Z}[x] / (q, \Phi_n)$ với $p$, $q$ và $n$ là các số nguyên tố như trên.

Khi $n$ là số nguyên tố thì $x^n - 1 = \Phi_1 \Phi_n$ và do đó $\mathcal{R}_p \cong \mathbb{Z}[x] / (p, \Phi_1) \times \mathcal{S}_p$ và $\mathcal{R}_q \cong \mathbb{Z}[x] / (q, \Phi_1) \times \mathcal{S}_q$.

Thông thường ta chọn $p = 3$ và $n = 701$. Việc chọn $n$ như vậy được (nhiều) người khẳng định là an toàn. Ở dưới ta viết $3$ thay vì $p$.

#### Tạo khóa

Đối với NTRU-HRSS-PKE, private key là một phần tử khác không $f \in \mathcal{S}_3$.

Từ $f$ ta tính public key $h = \Phi_1 \cdot g \cdot f^{-1} \in \mathcal{R}_q$ với một số $g \in \mathcal{S}_3$. Điều này đòi hỏi $f$ khả nghịch trong $\mathcal{R}_q$.

Để hỗ trợ giải mã ta cần nghịch đảo của $f$ trong $\mathcal{S}_3$. Để tránh nhầm lẫn, ta gọi nghịch đảo của $f$ trong $\mathcal{R}_q$ và $\mathcal{S}_3$ tương ứng là là $f^{-1}_q$ và $f^{-1}_3$.

Theo cấu trúc thì $f$ khả nghịch trong cả $\mathcal{S}_3$ và $\mathcal{S}_q$.

Thay vì lấy $f$ và $g$ trực tiếp từ $\mathcal{S}_3$ thì ta lấy từ tập con:

$$\mathcal{T}^+ = \{ v \in \mathcal{S}_3 : \langle xv, v \rangle \geqslant 0 \}$$

Thuật toán sinh khóa gồm các bước:

1. $f \gets \mathcal{T}^+$
2. $f^{-1}_3 \gets f^{-1} \in \mathcal{S}_3$
3. $f^{-1}_q \gets f^{-1} \in \mathcal{S}_q$
4. $g \gets \mathcal{T}^+$
5. $h = \Phi_1 \cdot g \cdot f^{-1} \in \mathcal{R}_q$
6. Trả về $\text{pk} = h$, $\text{sk} = (f, f^{-1}_3)$.

#### Mã hóa

Gọi $m \in \mathcal{S}_3$ là encode của thông điệp và $r \in \mathcal{S}_3$ được chọn ngẫu nhiên.

Input: $(m, h = \text{pk})$.

Output: ciphertext $e$ được tính:

$$e \gets p \cdot r \cdot h + [m]_3 \in \mathcal{R}_q$$

Ở đây $p = 3$ là số nguyên tố bên trên.

#### Giải mã

Input: $(e, (f, f^{-1}_3))$ và hai vành $(\mathcal{R}_q, \mathcal{S}_3)$.

Output: plaintext $m'$:

$$m' \gets [e \cdot f]_q \cdot f^{-1}_3 \in \mathcal{S}_3$$

Ở đây kí hiệu $[e \cdot f]_q$ nghĩa là phép tính diễn ra trong vành $\mathcal{R}_q$. Tương tự ở trên $[m]_3$ là encode của thông điệp $m$ trong $\mathcal{S}_3$.

## Phương pháp Coppersmith

Phương pháp Coppersmith được dùng để tìm nghiệm nhỏ của đa thức trên modulo. Phần này mình tham khảo chính từ {cite}`Galbraith`.

### Ý tưởng

Giả sử ta có phương trình $F(x) \equiv 0 \bmod M$​. Với số $X$​ cố định cho trước, phương pháp Coppersmith cho phép tìm nghiệm $x_0$ nhỏ thỏa mãn $\lvert x_0 \rvert \leqslant X$​.

Ý tưởng của phương pháp này là thay vì tìm nghiệm $x_0$ của $F(x)$​ trên modulo $M$​, chúng ta sẽ mở rộng lên, tìm một hàm $G(x)$​ nào đó mà có nghiệm $x_0$​ trên $\mathbb{Z}$​.

Đơn giản nhất là $G(x) = k \cdot F(x) + M \cdot g(x)$​, $k \in \mathbb{Z}$ và $\deg g(x) \leqslant \deg F(x)$. Rõ ràng khi modulo hai vế cho $M$​ thì $G(x_0) = F(x_0) = 0 \bmod M$.

Phương pháp này giúp tìm nghiệm của một đa thức bậc nhỏ modulo $M$​. Do đó giả sử đặt:

$$F(x) = a_0 + a_1 x + \cdots + a_d x^d$$
​
với $a_i \in \mathbb{Z}$.

Lúc này chúng ta sẽ tìm hàm $G(x)$​ trên với hệ số nhỏ.

Giả sử $g(x) = b_0 + b_1 x + \cdots + b_d x^d$ với $b_i \in \mathbb{Z}$.

Khi đó $G(x) = (k \cdot a_0 + M \cdot b_0) + (k \cdot a_1 + M \cdot b_1) x + \cdots + (k \cdot a_d + M \cdot b_d) x^d$. 

Ta mong muốn các hệ số $k \cdot a_0 + M \cdot b_0$​, $k \cdot a_1 + M \cdot b_1$​, $\cdots$​, $k \cdot a_d + M \cdot b_d$ nhỏ so với $M$​.

Do đó với số $X$​ cho trước, nếu ta xây lattice ($d+2$ vector) sau:

$$
	\begin{array}{cccccccc}
		\mathbf{v}_0 & \Leftarrow & M & 0 & 0 & \cdots & 0 & 0 \\
		\mathbf{v}_1 & \Leftarrow & 0 & MX & 0 & \cdots & 0 & 0 \\
		\vdots & \vdots & \vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\
		\mathbf{v}_d & \Leftarrow & 0 & 0 & 0 & \cdots & 0 & MX^d \\
		\mathbf{v}_{d+1} & \Leftarrow & a_0 & a_1 X & a_2 X^2 & \cdots & a_{d-1} X^{d-1} & a_d X^d
	\end{array}
$$

Khi đó hệ số của mỗi dòng từ $\mathbf{v}_0$​ tới $\mathbf{v}_d$​ là $b_0$​ tới $b_d$​. Còn hệ số của $\mathbf{v}_{d+1}$​ là $k$​.

Tuy nhiên chúng ta thường sẽ biến đổi để đa thức trở thành monic ($a_d = 1$​). Khi đó chúng ta bỏ đi $v_d$​ và còn $d+1$​ vector trong lattice.

### Cải tiến thuật toán

#### Dạng đơn giản

Giả sử $k(x)$​ có bậc là $h$​. Đặt $k(x) = c_0 + c_1 x + \cdots + c_h x^h$​.

Khi đó:

$$\begin{align*}
	G(x) = & k(x) \cdot F(x) + M \cdot g(x) \\
	= & (c_0 + c_1 x + \cdots c_h x^h) \cdot (a_0 + a_1 x + \cdots + x^d) + M \cdot (b_0 + b_1 x + \cdots + b_d x^d) \\
	= & c_0 \cdot F(x) + c_1 \cdot xF(x) + \cdots c_h \cdot x^h F(x) + M \cdot (b_0 + b_1 x + \cdots b_d x^d)
\end{align*}$$

Lúc này mỗi đại lượng $F(x)$​, $xF(x)$​, ...​, $x^h F(x)$​ sẽ khiến hệ số của $F(x)$​ ban đầu tăng bậc. Nói cách khác hệ số $a_i$ của $x^i$​ trong $F(x)$​ sẽ là hệ số của $x^{i+j}$​ trong $x^j F(x)$​.

Sách giáo khoa nói rằng nếu mình chọn $h=d-1$​ thì phương pháp Coppersmith sẽ cho ra kết quả nếu $X$​ được chọn thỏa $X \approx M^{1/(2d-1)}$.

Tương tự, mình sẽ có các vector trong lattice như sau:

$$
\begin{array}{ccccccccccc}
    \mathbf{v}_0 & \Leftarrow & M & 0 & 0 & \cdots & 0 & 0 & 0 & 0 & \cdots \\​
    \mathbf{v}_1 & \Leftarrow & 0 & MX & 0 & \cdots & 0 & 0 & 0 & 0 & \cdots \\
    \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots \\
    \mathbf{v}_{d-1} & \Leftarrow & 0 & 0 & 0 & \cdots & MX^{d-1} & 0 & 0 & 0 & \cdots \\
    \mathbf{v}_d & \Leftarrow & a_0 & a_1 X & a_2 X^2 & \cdots & a_{d-1} X^{d-1} & X^d & 0 & 0 & \cdots
\end{array}
$$

Sau đó thêm các vector khi shift vào, tương ứng với $xF(x)$​, $x^2 F(x)$​, ...​

$$
\begin{array}{cccccccccccc}
    \mathbf{v}_{d+1} & \Leftarrow & 0 & a_0 X & a_1 X^2 & a_2 X^3 & \cdots & a_{d-1} X^d & a_d X^{d+1} & 0 & 0 & \cdots \\
    \mathbf{v}_{d+2} & \Leftarrow & 0 & 0 & a_0 X^2 & a_1 X^3 & \cdots & a_{d-2} X^d & a_{d-1} X^{d+1} & a_d X^{d+2} & 0 & \cdots
\end{array}
$$

Tuy nhiên vấn đề ở đây là bound của nghiệm bị thu hẹp lại. Ban nãy mình nói rằng nếu chọn $h=d-1$​ thì nghiệm cho kết quả nếu $X \approx M^{1/(2d-1)}$​. Ở đây $M = 10001$​ nên $X \approx 4$​. Trong khi ở bài viết trước thì $X = 10$​. Do đó có thể thấy việc mở rộng này đôi khi kém hiệu quả tùy thuộc vào $h$​.

#### Dạng nâng cao

Coppersmith đã đề xuất ý tưởng như sau:

````{prf:lemma} Coppersmith
Với $0 < \epsilon < \min \{0,18; 1/d\}$. Đặt $F(x)$​ là đa thức monic bậc $d$​ có một hoặc nhiều nghiệm $x_0$​ trên modulo $M$​ sao cho $\lvert x_0 \rvert \leqslant \frac{1}{2} M^{1/d-\epsilon}$. Khi đó $x_0$​ có thể tính với thời gian đa thức giới hạn bởi $d$​, $1/\epsilon$​ và $\log(M)$.
````

Để chứng minh bổ đề này thì Coppersmith đã xây dựng một hệ lattice để tính toán và cũng là cách xây dựng lattice sẽ đề cập tới đây.

Chúng ta biết rằng $x_0$​ là nghiệm của đa thức $F(x) \equiv 0 \bmod M$​. Do đó ta suy ra $F(x_0)^k \equiv 0 \bmod M^k$​.

Từ nhận xét này, mình mở rộng phần cơ bản lên tìm nghiệm trong modulo $M^{h-1}$​ với $h$ là một số được chọn trước.

Với $k(x) = c_0 + c_1 x + \cdots + c_{d-1} x^{d-1}$ biểu diễn việc shift thành $F(x)$, $xF(x)$​, $x^2 F(x)$, ..., $x^{d-1} F(x)$​.

Ta xét $h$​ đa thức sau:

$$
\begin{array}{ccc}
    M^{h-1} F(x)^0 k(x) & \equiv & 0 \bmod M^{h-1} \\
    M^{h-2} F(x)^1 k(x) & \equiv & 0 \bmod M^{h-1} \\
    \cdots & \ddots & \cdots \\
    M^0 F(x)^{h-1} k(x) & \equiv & 0 \bmod M^{h-1}
\end{array}
$$

Với mỗi đa thức $M^{h-1-j} F(x)^j$​ chúng ta có $d$​ lần shift tương ứng với từng hệ số của $k(x)$​. Cụ thể là $M^{h-1-j}F(x)^j$​, $M^{h-1-j}F(x)^j x$​, $M^{h-1-j}F(x)^j x^2$​, ..., $M^{h-1-j}F(x)^j x^{d-1}$​.

Do đó có tất cả $dh$​ vector trong lattice. Số $h$​ thường được chọn sao cho $dh \approx \epsilon$. Và chặn nghiệm $X$​ có thể chọn là $\frac{1}{2}M^{1/d - \epsilon}$​ theo như bổ đề.

Như vậy mình xây lattice như sau:

- Bước 1. Với $M^{h-1} F(x)^0$​ thì các vector sau lần lượt tương ứng với

$$M^{h-1} F(x)^0, M^{h-1} F(x)^0 x, \ldots, M^{h-1} F(x)^0 x^{d-1}$$

Nói cách khác thì:

$$
\begin{array}{ccccccccc}
    \mathbf{v}_0 & \Leftarrow & M^{h-1} & 0 & 0 & \cdots & 0 & 0 & \cdots \\
    \mathbf{v}_1 & \Leftarrow & 0 & M^{h-1} X & 0 & \cdots & 0 & 0 & \cdots \\
    \vdots & \vdots & \vdots & \vdots & \vdots & \ddots & \vdots & \vdots & \vdots \\
    \mathbf{v}_{d-1} & \Leftarrow & 0 & 0 & 0 & \cdots & M^{h-1} X^{d-1} & 0 & \cdots
\end{array}
$$

- Bước 2. Với $M^{h-2} F(x)$​ thì các vector sau lần lượt tương ứng với

$$M^{h-2} F(x)^1, M^{h-2} F(x)^1 x, \ldots, M^{h-2} F(x)^1 x^{d-1}$$

Nói cách khác thì:

$$
\begin{array}{cccccccccc}
    \mathbf{v}_d & \Leftarrow & Ma_0 & M a_1 X & M a_2 X^2 & \cdots & M a_{d-1} X^{d-1} & M X^d & \cdots & \cdots \\ 
    \mathbf{v}_{d+1} & \Leftarrow & 0 & Ma_0 X & Ma_1 X^2 & \cdots & M a_{d-2} X^{d-1} & M a_{d-1} X^d & M X^{d+1} & \cdots \\
    \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots \\
    \mathbf{v}_{2d-1} & \Leftarrow & 0 & 0 & 0 & \cdots & M a_0 X^{d-1} & M a_1 X^d & \cdots & \cdots
\end{array}
$$

- Bước thứ $j$. Cứ như vậy với $M^{h-1-j}F(x)^j$​.

Chạy LLL trên lattice trên sẽ cho kết quả 😆

