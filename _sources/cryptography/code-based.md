# Code-based cryptography

```{contents}
:depth: 2
```

## Introduction

````{prf:definition} Block code
**Block code** $(n)_q$ (error-correcting code) là tập hợp $\mathcal{C}$ bất kì chứa các vector độ dài $n$ trên trường $\mathbb{F}_q$.
````

````{prf:definition} Codeword
**Codeword** (từ mã) là bất kì vector nào trong block code $\mathcal{C}$.
````

````{prf:definition} Lực lượng của code
**Lực lượng** (hay **cardinality**) $M$ của code $\mathcal{C}$ là số lượng codeword trong $\mathcal{C}$. Kí hiệu $M = \lvert C \rvert$.
````

````{prf:definition} 
Block code $\mathcal{C}$ trên trường $\mathbb{F}_q$ có độ dài $n$ và có lực lượng $M$ được gọi là $(n, M)_q$ code.
````

````{prf:definition} Độ dài của code
Độ dài của $(n)_q$ code $\mathcal{C}$ là số $n$ chỉ độ dài mỗi codeword (độ dài vector).
````

````{prf:definition} Khoảng cách tối thiểu
**Khoảng cách tối thiểu** (hay **minimum distance**) của code $\mathcal{C}$ là số $d$ chỉ khoảng cách Hamming nhỏ nhất giữa hai codeword trong code $\mathcal{C}$:

$$d = \min_{u, v \in \mathcal{C}, u \neq v} \rho(u, v) = \min_{u, v \in \mathcal{C}, u \neq v} \mathrm{wt}(u - v).$$
````

Nhắc lại, khoảng cách Hamming của một vector là số phần tử khác $0$ trong vector đó:

$$\mathrm{wt}(x_1, x_2, \ldots, x_n) = \#\{ x_i \mid x_i \neq 0 \}.$$

````{prf:definition} 
Block code $\mathcal{C}$ trên trường $\mathbb{F}_q$ với độ dài $n$, lực lượng $M$ và có khoảng cách tối thiểu $d$ được gọi là $(n, M, d)_q$ code.
````

Thông tin ban đầu có thể được chia thành các đoạn độ dài $k$ và mỗi đoạn như vậy được encode thành một đoạn độ dài $n$. 

Cụ thể hơn, **hàm encode** biến đổi một thông điệp $a$ độ dài $k$ thành codeword $c \in \mathcal{C}$ với độ dài $n$:

$$\varphi: V_k(q) \to \mathcal{C}, \quad \varphi(a) = c.$$

Ánh xạ $\varphi$ cần là đơn ánh (one-to-one) vì chúng ta không muốn hai thông điệp độ dài $k$ cùng encode ra một codeword độ dài $n$  (khi decode chúng ta không biết sẽ ra thông điệp nào).

````{prf:lemma} 
Để $(n, M)_q$ code có thể encode được các thông điệp độ dài $k$ thì điều kiện cần và đủ để tồn tại ánh xạ $\varphi$ như trên là $k \leqslant \lfloor \log_q M \rfloor$.
````

````{prf:definition} Спектр весов
**Phổ trọng số** (hay **спектр весов**) của $(n)_q$ code $\mathcal{C}$ là một vector các số nguyên không âm $(A_0, A_1, \ldots, A_n) \in \mathbb{Z}^{n+1}_{\geqslant 0}$ với $A_i$ là số lượng vector có trọng số Hamming bằng $i$ trong code.
````

## Bài toán decode tổng quát

Khi vector $x$ được truyền qua kênh truyền, không gì đảm bảo chúng ta sẽ nhận được chính xác $x$ ở bên nhận, mà có thể là $y$ nào đó.

Các codeword nằm trong một block code nào đó là tập con của $V_n(q)$, trong khi ở bên nhận có thể là một vector bất kỳ trong $V_n(q)$. Bài toán decode đặt ra câu hỏi, làm sao biết được vector $y$ sẽ được decode thành vector nào trong block code.

````{prf:definition} Bài toán decode
Bài toán decode của $(n)_q$ code $\mathcal{C}$ là bài toán cho trước vector $y \in V_n(q)$, ta tìm codeword $c \in \mathcal{C}$ của code $(n)_q$ sao cho $\displaystyle{\rho_H (c,y) = \min_{c' \in \mathcal{C}} \rho_H (c', y)}$ với $\rho_H$ là khoảng cách Hamming.
 
**Input:** vector $y \in V_n(q)$ nhận được từ kênh truyền; $\mathcal{C}$ là $(n)_q$ code.

**Output:** vector $c \in \mathcal{C}$ là codeword sao cho $\displaystyle{\rho_H (c, y) = \min_{c' \in \mathcal{C}} \rho_H(c', y)}$.
````

````{prf:definition} Bài toán decode
Bài toán decode của $(n)_q$ code $\mathcal{C}$ là bài toán cho trước vector $y \in V_n(q)$, ta tìm codeword $c \in \mathcal{C}$ của code $(n)_q$ sao cho $\displaystyle{\mathrm{wt}(y - c) = \min_{c' \in \mathcal{C}} \mathrm{wt}(y - c')}$ với $\mathrm{wt}$ là trọng số Hamming.

**Input:** vector $y \in V_n(q)$ là vector nhận được từ kênh truyền; $\mathcal{C}$ là $(n)_q$ code.

**Output:** vector $c \in \mathcal{C}$ là codeword sao cho $\displaystyle{\mathrm{wt}(y - c) = \min_{c' \in \mathcal{C}} \mathrm{wt} (y - c')}$.
````

````{prf:definition} Bài toán decode
Bài toán decode của $(n)_q$ code $\mathcal{C}$ là bài toán cho trước vector $y \in V_n(q)$, ta tìm vector $e \in V_n(q)$ sao cho $y - e \in \mathcal{C}$, nghĩa là $y - e$ là codeword, và vector $e$ có trọng số Hamming nhỏ nhất $\mathrm{wt}(e) \to \min$.

**Input:** vector $y \in V_n(q)$ là vector nhận được từ kênh truyền; $\mathcal{C}$ là $(n)_q$ code.

**Output:** vector $e \in V_n(q)$ sao cho $y - e \in \mathcal{C}$, nghĩa là $y - e$ là codeword, và vector $e$ có trọng số Hamming nhỏ nhất $\mathrm{wt}(e) \to \min$.
````

````{prf:remark} 
Các định nghĩa về bài toán decode ở trên tương đương nhau.
````

````{prf:definition} Decoder
**Decoder** của code $(n)_q$ $\mathcal{C}$ là thuật toán mà với vector $y \in V_n(q)$ cho trước, tìm được codeword $c \in \mathcal{C}$ sao cho vector $e = y - c$ có trọng số Hamming nhỏ nhất có thể, nghĩa là $\displaystyle{c = \underset{u \in \mathcal{C}}{\operatorname{argmin}} \mathrm{wt}(y - u)}$. Decoder của code $\mathcal{C}$ sẽ giải bài toán decode trên code $\mathcal{C}$.
````

## Mã tuyến tính (Linear code)

````{prf:definition} Mã tuyến tính, Linear code
Block code $(n)_q$ $\mathcal{C}$ được gọi là **tuyến tính** (hay **linear**) nếu với mọi $a, b \in \mathbb{F}_2$ và với mọi codeword $x, y \in \mathcal{C}$ thì vector $a \cdot x + b \cdot y$ cũng là codeword thuộc $\mathcal{C}$.
````

Ta kí hiệu mã tuyến tính là $[n]_q$. Có thể thấy blockcode $[n]_q$ là không gian vector con của $V_n(q)$.

````{prf:definition}  
Đối với code $[n]_q$ thì số $n$ được gọi là **độ dài** của code.
````

````{prf:definition}  
**Số chiều** của code $[n]_q$ là số $k$ bằng với số chiều của không gian vector con $\mathcal{C}$ của $V_n(q)$.
````

````{prf:definition}  
Mã tuyến tính $\mathcal{C}$ có độ dài $n$ và số chiều $k$ được gọi là $[n, k]_q$ code.
````

````{prf:definition}  
**Tốc độ truyền** của $[n, k]_q$ code là số $R = \dfrac{k}{n}$.
````

````{prf:definition}  
**Redundancy** (hay **избыточность**) của $[n, k]_q$ code là số $r = n - k$.
````

````{prf:definition}  
**Khoảng cách nhỏ nhất** của code $\mathcal{C}$ là số $d$ bằng với trọng số Hamming nhỏ nhất của các codeword trong $\mathcal{C}$

$$d = \min_{u \in \mathcal{C}, u \neq 0} \mathrm{wt}(u)$$
````

````{prf:definition}  
Mã tuyến tính $[n, k]_q$ với khoảng cách nhỏ nhất $d$ được gọi là $[n, k, d]_q$ code.
````

### Ma trận sinh

````{prf:definition}  
Ma trận $G$ được gọi là **ma trận sinh** (hay **порождающая матрица**) của code $C$ nếu nó chứa các vector trong cơ sở của không gian vector con $\mathcal{C}$.
````

Nếu $\mathcal{C}$ là $[n, k]_q$ code thì $G$ là ma trận kích thước $k \times n$.

````{prf:remark} 
Nếu $G$ là ma trận sinh của $[n, k]_q$ code thì

$$\mathcal{C} = \{ a \cdot G \mid a \in V_k(q) \}$$
````

Ở đây ta nói ma trận $G$ sinh ra code $\mathcal{C}$.

Theo kiến thức đại số tuyến tính, nếu $G_1$ và $G_2$ kích thước $k \times k$ cùng sinh ra một code $\mathcal{C}$ thì tồn tại ma trận nghịch đảo $A$ kích thước $k \times k$ trên $\mathbb{F}_q$ sao cho $A G_1 = G_2$.

### Coder

````{prf:definition}  
**Coder** $\varphi : V_k(q) \to V_n(q)$ cho $[n, k]_q$ code xác định bởi ma trận sinh $G$ theo nghĩa:

$$\varphi((a_1, \ldots, a_k)) = (a_1, \ldots, a_k) \cdot G$$
````

````{prf:definition} 
Ma trận $G$ kích thước $k \times n$ được gọi là **systematic** nếu nó có dạng:

$$G = (I_k \Vert G_0)$$

với $I_k$ là ma trận đơn vị $k \times k$ và $G_0$ là ma trận cỡ $(k \times (n - k))$ nào đó.
````

````{prf:definition}  
Code được gọi là **systematic** nếu nó có ma trận sinh $G$ là systematic.
````

````{prf:definition} 
Coder $\varphi_G$ của systematic code $[n, k]_q$, xác định bởi ma trận sinh systematic $G = (I_k \Vert G)$, được gọi là **systematic**.
````

Khi đó với mọi thông điệp $a = (a_1, \ldots, a_k) \in V_k(q)$ thì coder thực hiện:

$$a = (a_1, \ldots, a_n) \xrightarrow{\varphi} (a_1, \ldots, a_k, a \cdot G_0)$$

Lưu ý rằng không phải code nào cũng là systematic và do đó không tồn tại systematic coder.

````{prf:definition}  
Ta đánh số tọa độ các codeword trong $[n, k]_q$ code từ $1$ tới $n$. **Tập thông tin** (hay **information set**, **информационное множество**) $\mathcal{I}$ của code $[n, k]_q$ là tập con của tập đánh số tọa độ, nghĩa là $\mathcal{I} \subseteq \{ 1, \ldots, n \}$, sao cho $\lvert \mathcal{I} \rvert = k$ và ma trận con $G_k$ kích thước $k \times k$ của ma trận sinh $G$ thì khả nghịch.
````

### Ma trận kiểm tra

````{prf:definition}  
Nếu $\mathcal{C}$ là nhân của ma trận $H$, tức là

$$\mathcal{C} = \ker(H) = \{ v \in \mathcal{C}: H v^\top = 0 \}$$

thì ta nói $H$ là **ma trận kiểm tra chẵn lẻ** (hay **parity-check matrix**).
````

Ta có thể thấy $G H^\top = 0$.

````{prf:definition}  
**Syndrome** $S_H(y)$ của vector $y \in V_n(q)$ tương ứng với ma trận parity-check $H$ của $[n, k]_q$ code $\mathcal{C}$ là vector cột $S_H(y) = H \cdot y^\top$. Khi đó $S_H(y)$ có độ dài $r = n - k$ - chính là redundancy ở trên.
````

````{prf:remark} 
Nếu $H_1$ và $H_2$ là hai ma trận parity-check của code $\mathcal{C}$ thì $S_{H_1}(y) = A \cdot S_{H_2}(y)$ với $A$ là ma trận khả nghịch thỏa mãn $H_2 = A \cdot H_1$.
````

### Mã tuyến tính

Do $[n]_q$ code cũng là $(n)_q$ code nên ta cũng có định nghĩa phổ trọng số như $(n)_q$:

````{prf:definition}  
**Спектр весов** của $[n]_q$ code $\mathcal{C}$ là vector $(A_0, A_1, \ldots, A_n) \in \mathbb{Z}^{n+1}_{\geqslant 0}$ với $A_i \geqslant 0$ là số lượng vector có trọng số bằng $i$ trong code.
````

### Dual code (mã đối ngẫu) và kiểm tra chẵn lẻ (check-parity)

````{prf:definition} 
**Mã đối ngẫu** (hay **dual code**, **дуальный код**) của mã tuyến tính $\mathcal{C}$ là code $\mathcal{C}^\top$ được sinh bởi parity-check matrix $H$ của code $\mathcal{C}$.
````

````{prf:remark} 
Mã đối ngẫu với $[n, k]_q$ code là $[n, n-k]_q$ code.
````

````{prf:remark} 
Với mọi mã $\mathcal{C}$ ta có $(\mathcal{C}^\top)^\top = C$.
````

````{prf:remark} 
Với mọi $[n]_q$ code $\mathcal{C}$ và $\mathcal{B}$ thì ta có đẳng thức:

$$(\mathcal{C} + \mathcal{B})^\top = \mathcal{C}^\top \cap \mathcal{B}^\top.$$

Trong đó $\mathcal{C} + \mathcal{B} = \{ u + v : u \in \mathcal{C}, v \in \mathcal{B} \}$ - tổng của hai code $\mathcal{C}$ và $\mathcal{B}$.
````

````{prf:definition}  
Với các vector $x = (x_1, \ldots, x_n)$ và $y = (y_1, \ldots, y_n)$ trong $V_n(q)$ ta định nghĩa **tích vô hướng** (hay **inner product**, **dot product**, **скалярное произведение**) của hai vector là:

$$\langle x, y \rangle = x_1 y_1 + \ldots + x_n y_n \in \mathbb{F}_q$$
````

````{prf:definition} 
Vector $h \in V_n(q)$ được gọi là **parity-check** (hay **проверка на чётность**) của $[n]_q$ code nếu với mọi $c \in \mathcal{C}$ ta có $\langle c, h \rangle = 0$, nói cách khác vector $h$ trực giao với mọi vector $c \in \mathcal{C}$.
````

````{prf:remark} 
Mã đối ngẫu $\mathcal{C}^\top$ trùng với tập tất cả parity-check vector của code $\mathcal{C}$.
````

## Bài toán decode trên mã tuyến tính

````{prf:definition} 
**Bài toán decode trên mã tuyến tính $[n, k]_q$ với ma trận sinh $G$ trong điều kiện kênh truyền có $t$ lỗi** là bài toán cho trước vector $y \in V_n(q)$, ta tìm vector $m \in V_k(q)$ sao cho vector $e = y - m G$ có trọng số Hamming bằng $t$.

**Input:** vector $y \in V_n(q)$, ma trận sinh $G$ cỡ $k \times n$, số tự nhiên $t \in \mathbb{N}$.

**Output:** vector $m \in V_k(q)$ sao cho vector $e = y - m G$ có trọng số Hamming bằng $t$.
````

````{prf:definition}  
**Bài toán decode trên mã tuyến tính $[n, k]_q$ với ma trận parity-check $H$ trong điều kiện kênh truyền có $t$ lỗi** là bài toán cho trước vector $y \in V_n(q)$, ta tìm vector $e \in V_n(q)$ sao cho $e H^\top = y H^\top$ và vector $e$ có trọng số Hamming bằng $t$, hay $\mathrm{wt}(e) = t$.

**Input:** vector $y \in V_n(q)$, ma trận parity-check $H$ cỡ $(n - k) \times n$ và số tự nhiên $t \in \mathbb{N}$.

**Output:** vector $e \in V_n(q)$ có trọng số Hamming bằng $t$, hay $\mathrm{wt}(e) = t$, sao cho $e H^\top = y H^\top$.
````

Từ các bài toán decode mã tuyến tính liên hệ với bài toán decode syndrome code.

````{prf:definition} 
**Bài toán tối ưu** (hay **bài toán tổng quát**) của syndrome decode $[n, k]_q$ với ma trận parity-check $H$ là bài toán cho trước vector $s \in V_n(q)$, ta tìm vector $e \in V_n(q)$ sao cho $H e^\top = s^\top$ và vector $e$ có trọng số Hamming nhỏ nhất có thể, hay $\mathrm{wt}(e) \to \min$.

**Input:** 

- $s \in V_n(q)$ - syndrome
- $H$ là ma trận parity-check cỡ $(n - k) \times n$ của $[n, k]_q$ code $\mathcal{C}$

**Output:**

- vector $e \in V_n(q)$ thỏa mãn $H e^\top = s^\top$ và vector $e$ có trọng số Hamming nhỏ nhất có thể, hay $\mathrm{wt}(e) \to \min$.
````

````{prf:definition} 
**Bài toán tìm kiếm syndrome decode** $sSD(H, s, t)$ là bài toán tìm kiếm theo vector $s \in V_r(q)$ vector $e \in V_n(q)$ có trọng số Hamming bằng $t$, hay $\mathrm{wt}(e) = t$ và $H e^\top = s^\top$.

**Input:**

- $H$ là ma trận cỡ $r \times n$ trên $\mathbb{F}_q$
- $s \in V_r(q)$ là syndrome
- $t \in \mathbb{N}$ là trọng số Hamming

**Output:** vector $e \in V_n(q)$ có trọng số Hamming bằng $t$, hay $\mathrm{wt}(e) = t$, và $H e^\top = s^\top$.
````

````{prf:definition} 
**Bài toán nhận dạng syndrome decode** (hay **распознавательная задача синдромного декодирования**) hay đơn giản là **bài toán syndrome decode** (hay **задача синдромного декодирования**) $SD(H, s, t)$ là bài toán xác định theo syndrome $s \in V_r(q)$ xem có tồn tại hay không vector $e \in V_n(q)$ có trọng số Hamming bằng $t$ và thỏa mãn $H e^\top = s^\top$.

**Input:**

- $H$ là ma trận cỡ $r \times n$ trên $\mathbb{F}_q$
- $s \in V_r(q)$ là syndrome
- $t \in \mathbb{N}$ là trọng số Hamming

**Output:** có tồn tại hay không vector $e \in V_n(q)$ có trọng số Hamming $\mathrm{wt} (e) = t$ và thỏa $H e^\top = s^\top$.
````

````{prf:theorem}
(Theo {cite}`1055873`) Bài toán nhận dạng syndrome code $SD(H, s, t)$ là NP-complete.
````

## Bài toán phổ trọng số của mã tuyến tính

````{prf:definition} 
**Bài toán về phổ trọng số của mã tuyến tính** (hay **Задача о спектре весов линейного кода**) $WS(H, t)$ là bài toán nhận dạng trong code, với ma trận parity-check $H$, có tồn tại hay không vector $c \in V_n(q)$ có trọng số Hamming bằng $t$ và thỏa mãn $H c^\top = 0$.
````

````{prf:theorem}  
(theo {cite}`1055873`) Bài toán về phổ trọng số là NP-complete.
````

## Ý tưởng xây dựng các hệ mật mã dựa trên mã sửa sai

Đặt $G$ là ma trận sinh của mã tuyến tính $[n, k]_q$ $\mathcal{C}$ có thể sửa $t$ lỗi.

Nếu code với ma trận sinh $G$ không có các cấu trúc đại số hoặc tổ hợp thì theo định lí trên về độ khó NP của bài toán nhận dạng syndrome decode, bài toán decode mã tuyến tính $[n, k]_q$ là rất khó.

Khi đó nếu mã hóa thông điệp $m$ có thể thực hiện qua việc: $m \to c = m G + e$, $\mathrm{wt}(e) = t$, $e \in V_n(q)$.

Khi đó, cho trước vector $c$, việc tìm một vector $m$ là bài toán decode trên mã tuyến tính $[n, k]_q$ với ma trận sinh $G$, không có các cấu trúc đại số hoặc tổ hợp. Suy ra việc phá mã rất khó.

Vấn đề là ở phía bên việc tìm lại $m$ từ $c$ rất khó nên cần một phương án để decrypt lại thông điệp ban đầu.

## Bài toán tương đương các mã tuyến tính

### Hoán vị và tác động của chúng lên tập hợp

````{prf:definition} (Hoán vị)
Xét $N$ là tập hợp có $n$ phần tử. Khi đó một **hoán vị** (hay **permutation**, **постановка**) $\sigma: N \to N$ là một song ánh từ $N$ tới $N$. Tập hợp tất cả hoán vị trên tập $N$ được kí hiệu là $\mathcal{S}_N$. Nếu $N = \{ 1, 2, \ldots, n \}$ thì ta có thể viết $\mathcal{S}_N = \mathcal{S}_n$.
````

Đặt $\sigma \in \mathcal{S}_n$ là một hoán vị trên tập $\{ 1, \ldots, n \}$. Khi đó ta định nghĩa tác động của hoán vị $\sigma$ lên vector $x \in V_n(q)$. Giả sử vector $x = (x_1, \ldots, x_n) \in V_n(q)$, ta định nghĩa tác động của hoán vị $\sigma$ lên vector $x$ như sau:

$$x^\sigma = (x_{\sigma(1)}, x_{\sigma(2)}, \ldots, x_{\sigma(n)})$$

Có thể thấy tác động của $\sigma$ lên $V_n(q)$ là tuyến tính, nghĩa là với mọi $\alpha, \beta \in \mathbb{F}_q$ và với mọi vector $x, y \in V_n(q)$ ta có:

$$(\alpha \cdot x + \beta \cdot y)^\sigma = \alpha \cdot x^\sigma + \beta \cdot y^\sigma$$

Nếu $U \subseteq V_n(q)$ thì kí hiệu $U^\sigma$ là tác động của hoán vị $\sigma$ lên mỗi vector trong $U$, nghĩa là $U^\sigma = \{ x^\sigma \mid x \in U \}$.

Do tính tuyến tính của tác động từ $\mathcal{S}_n$ lên $V_n(q)$, nếu $\mathcal{C}$ là $[n, k, d]_q$ code thì $\mathcal{C}^\sigma$ cũng là $[n, k, d]_q$ code.

Mỗi hoán vị $\sigma \in \mathcal{S}_n$ có thể được viết thành dạng ma trận $n \times n$ là $P_\sigma = (p_{ij})$. Khi đó phần tử $p_{ij} = 1$ nếu $\sigma(j) = i$, các vị trí còn lại bằng $0$.

````{prf:example} 
Với hoán vị $\sigma = \begin{pmatrix} 1 & 2 & 3 & 4 & 5 \\ 4 & 1 & 5 & 3 & 2 \end{pmatrix}$ thì ma trận tương ứng là:

$$P_\sigma = \begin{pmatrix}
    0 & 1 & 0 & 0 & 0 \\
    0 & 0 & 0 & 0 & 1 \\
    0 & 0 & 0 & 1 & 0 \\
    1 & 0 & 0 & 0 & 0 \\
    0 & 0 & 1 & 0 & 0
\end{pmatrix}$$

Khi đó tác động của $\sigma$ lên vector $x$ là $x^\sigma = x \cdot P_\sigma$.

Như vậy, với mọi vector $x = (x_1, x_2, x_3, x_4, x_5)$, dưới tác động của $\sigma$ bên trên ta có:

$$x^\sigma = (x_{\sigma(1)}, x_{\sigma(2)}, x_{\sigma(3)}, x_{\sigma(4)}, x_{\sigma(5)}) = (x_4, x_1, x_5, x_3, x_2)$$

Ta cũng thấy phép nhân vector $x$ với ma trận $P_\sigma$ cho kết quả:

$$x \cdot P_\sigma = (x_4, x_1, x_5, x_3, x_2)$$
````

### Mã tương đương và nhóm các automorphism của mã tuyến tính

````{prf:definition} 
Hai $[n]_q$ code $\mathcal{C}_1$ và $\mathcal{C}_2$ được gọi là **tương đương** (hay **tương đương hoán vị**, **перестановочно эквивалентные**) nếu tồn tại một hoán vị $\sigma \in \mathcal{S}_n$ sao cho $\mathcal{C}_1 = \mathcal{C}_2^\sigma$.
````

````{prf:definition} 
Hai ma trận $G_1$ và $G_2$ kích thước $k \times n$ gọi là **tương đương hoán vị** nếu tồn tại ma trận $M$ cỡ $k \times k$ và hoán vị $\sigma \in \mathcal{S}_n$ sao cho $M \cdot G_1 = G_2 \cdot \sigma$.
````

### Nhóm các automorphism của code

````{prf:definition} 
**Automorphism** của $(n)_q$ code $\mathcal{C}$ là hoán vị $\sigma$ sao cho $\mathcal{C} = \mathcal{C}^\sigma$. Tập hợp tất cả automorphism của code $\mathcal{C}$ được kí hiệu là nhóm $PAut(\mathcal{C})$ và được gọi là **nhóm automorphism hoán vị** hoặc đơn giản hơn là **nhóm automorphism** của code $\mathcal{C}$.
````

### Bài toán về tính tương đương giữa các mã tuyến tính nhị phân

````{prf:definition} 
**Bài toán về tính tương đương giữa các mã tuyến tuyến tính** là bài toán nhận dạng tính chất tương đương giữa hai mã tuyến tính $[n]_q$ $\mathcal{C}_1$ và $\mathcal{C}_2$ với ma trận sinh tương ứng là $G_1$ và $G_2$.

**Input:** hai ma trận $G_1$ và $G_2$ cỡ $k \times n$.

**Output:** hai ma trận $G_1$ và $G_2$ có tương đương hoán vị hay không.
````

Sau đây chúng ta xem xét code nhị phân, tức $q = 2$.

````{prf:definition} 
:class: dropdown
**Interactive proof** cho ngôn ngữ $L \subseteq \{ 0, 1 \}^\star$ là cặp thuật toán (máy Turing) $(\mathcal{P}, \mathcal{V})$ thỏa mãn các điều kiện sau:

1. $\mathcal{P}$ (**prover**) là bất kì máy Turing nào có tape riêng.
2. $\mathcal{V}$ (**verifier**) là máy Turing xác suất đa thức có tape riêng.
3. $\mathcal{P}$ và $\mathcal{V}$ có chung tape, nói cách khác là **tương tác** (hay **interactive**).
4. 5. 6. 7. Các điều kiện sẽ được nói sau.
````

````{prf:algorithm}  Interactive proof (Интерактивное доказательство) cho ngôn ngữ $cLEC$
:class: dropdown
**Input:** ma trận $G_1$ và $G_2$ cỡ $k \times n$ trên $\mathbb{F}_2$

**Output:** hoặc $G_1 \not\sim G_2$ , hoặc $G_1 \sim G_2$

1. $m \gets 2n \cdot k$
2. $\mathcal{V}$ chọn ngẫu nhiên (theo phân bố đều) $m$ số $i_l \in \{ 1, 2 \}$ với $l = 1, \ldots, m$
3. $\mathcal{V}$ chọn ngẫu nhiên (theo phân bố đều) các ma trận khả nghịch $M_l$ cỡ $k \times k$ với $l = 1, \ldots, m$ và các hoán vị $\sigma_l \in \mathcal{S}_n$ với $l = 1, \ldots, m$
4. $\mathcal{V}$ tính $F_l = M_l G_{i_l} \sigma_l$ với $l = 1, \ldots, m$
5. $\mathcal{V} \to \mathcal{P} : (F_1, \ldots, F_m)$
6. $\mathcal{P}$: với mỗi ma trận $F_l$, $l = 1, \ldots, m$, tính ma trận $G_{j_l}$ với $j_l \in \{ 1, 2 \}$ mà tương đương với $F_l$. Nếu không thể tính được thì verifier chọn ngẫu nhiên $j_l \in \{ 1, 2 \}$
7. $\mathcal{P} \to \mathcal{V} : (j_1, \ldots, j_m)$
8. $\mathcal{V}$: nếu với mọi $l = 1, \ldots, m$ thỏa đẳng thức $i_l = j_l$ thì verifier trả về kết quả $G_1 \not\sim G_2$. Trường hợp ngược lại trả về $G_1 \sim G_2$
````

### Định lí về polynomial-time reduction của bài toán đẳng cấu đồ thị đến bài toán sự tương đương của mã

````{prf:definition} 
**Ma trận kề** (hay **матрица инцидентности**) là ma trận nhị phân $D = (d_{ev})$ cỡ $\lvert E \rvert \times \lvert V \rvert$, với $d_{ev} = 1$ nếu $e = (u, v)$ với $v$ nào đó thuộc $V$, nghĩa là $d_{ev} = 1$ khi và chỉ khi trên đồ thị có cạnh $e$ xuất phát từ đỉnh $v$.
````

````{prf:definition} 
Hai đồ thị $(E_1, V_1)$ và $(E_2, V_2)$ được gọi là **đẳng cấu** (hay **isomorphism**) nếu tồn tại song ánh $\varphi : V_1 \to V_2$ sao cho với mọi cặp đỉnh $(u, v) \in E_1$ thì cặp $(\varphi(u), \varphi(v)) \in E_2$.
````

````{prf:definition} 
Bài toán xác định hai đồ thị, xác định bởi ma trận kề, có đẳng cấu với nhau hay không.

**Input:** hai ma trận nhị phân $D_1$ và $D_2$ cỡ $k \times n$.

**Output:** có tồn tại hay không các hoán vị $\gamma \in \mathcal{S}_k$ và $\sigma \in \mathcal{S}_n$ sao cho $D_1 = \gamma \cdot D_2 \cdot \sigma$.
````

## Các hệ mật mã khóa công khai dựa trên lý thuyết mã

### Hệ mật mã McEliece

Hệ mật mã McEliece được phát triển bởi R.J. Mceliece vào năm 1978 trong {cite}`McEliece1978APK`.

#### Ý tưởng xây dựng

Đặt $G$ là ma trận sinh của mã tuyến tính $[n, k]_q$ $\mathcal{C}$ nào đó, sửa được $t$ lỗi.

#### Tham số

- $\mathcal{C} = \{ \mathcal{C}_\lambda \}_{\lambda \in \Lambda}$ là một họ các mã tuyến tính trên trường $\mathbb{F}_q$ sao cho với mỗi code $C \in \mathcal{C}$ có một thuật toán decode hiệu quả là $Decode$ sửa được $t$ lỗi. Ở đây $\Lambda \subseteq \{ 0, 1 \}^\star$ là tập các giá trị của tham số code trong họ.
- $Sample(1^\lambda)$ là thuật toán xác suất hiệu quả và детерминированный, sao cho với giá trị tham số $\lambda \in \Lambda$ cho ra ma trận sinh $G$ của code $\mathcal{C}_\lambda$, số lượng lỗi $t$ và thuật toán $Decode$, giải được bài toán decode trên mã tuyến tính $[n, k]_q$ với ma trận sinh $G$ và kênh truyền có $t$ lỗi. Kí hiệu $\mathcal{G} = \{ G_\lambda \}_{\lambda \in \Lambda}$ là tập tất cả ma trận sinh cho ra thuật toán $Sample(1^\lambda)$ cho mọi trường hợp tham số $\lambda \in \Lambda$.

#### Thuật toán sinh khóa (Gen)

Private key gồm:

1. Ma trận $M \in \mathrm{GL}_q(k)$ không suy biến cỡ $k \times k$ trên $\mathbb{F}_q$
2. $G \in V_{k \times n}(q)$ là ma trận sinh của $[n, k]_q$ code $\mathcal{C}_\lambda$
3. $P \in \mathcal{S}_n$ là hoán vị trên tập $\{ 1, \ldots, n \}$
4. $Decode$ là thuật toán decode trên mã $\mathcal{C}_\lambda$
5. $t$ là số lỗi được sửa bởi thuật toán $Decode$

Public key gồm:

1. $G_{pub} = M \cdot G \cdot P \in V_{k \times n}(q)$ là ma trận sinh của code tương đương với code $\mathcal{C}_\lambda$
2. $t \in \mathbb{N}$ là số lỗi được decode bởi $Decode$

#### Thuật toán mã hóa (Enc)

Thuật toán mã hóa nhận đầu vào là thông điệp $m \in V_k(q)$ và trả về ciphertext $c \in V_n(q)$.

Để mã hóa, chọn ngẫu nhiên vector $e \in V_n(q)$ độ dài $n$ và có trọng số Hamming bằng $t$. Khi đó ta tính ciphertext:

$$c = m \cdot G_{pub} + e$$

#### Thuật toán giải mã (Dec)

1. Tính $b \gets c \cdot P^{-1}$
2. Tính $u \gets Decode(b)$
3. Tính $m \gets u \cdot M^{-1}$

Khi đó $m$ là plaintext ban đầu.

### Hệ mật mã Niederreiter

#### Tham số

- $\mathcal{C} = \{ \mathcal{C}_\lambda \}_{\lambda \in \Lambda}$ là một họ các mã tuyến tính trên trường $\mathbb{F}_q$ sao cho với mỗi code $C \in \mathcal{C}$ có một thuật toán decode hiệu quả là $Decode$ sửa được $t$ lỗi. Ở đây $\Lambda \subseteq \{ 0, 1 \}^\star$ là tập các giá trị của tham số code trong họ.
- $Sample(1^\lambda)$ là thuật toán xác suất hiệu quả và детерминированный, sao cho với giá trị tham số $\lambda \in \Lambda$ cho ra ma trận parity-check $H$ của code $\mathcal{C}_\lambda$, số lượng lỗi $t$ và thuật toán $SDecode$, giải được bài toán syndrome decode trên mã tuyến tính $[n, k]_q$ với ma trận parity-check $H$ và kênh truyền có $t$ lỗi. Kí hiệu $\mathcal{H} = \{ H_\lambda \}_{\lambda \in \Lambda}$ là tập tất cả ma trận parity-check cho ra thuật toán $Sample(1^\lambda)$ cho mọi trường hợp tham số $\lambda \in \Lambda$.

#### Thuật toán sinh khóa (Gen)

Private key gồm:

1. Ma trận $M \in \mathrm{GL}_q(r)$ cỡ $r \times r$ trên $\mathbb{F}_q$, với $r = n - k$ là số kí tự kiểm tra của $[n, k]_q$ code $\mathcal{C}_\lambda$.
2. $H \in V_{r \times n}(q)$ là ma trận parity-check của $[n, k]_q$ code $\mathcal{C}_\lambda$.
3. $P \in \mathcal{S}_n$ là hoán vị trên $\{ 1, \ldots, n \}$
4. $SDecode$ là thuật toán syndrome decode trên code $\mathcal{C}_\lambda$.
5. $t$ là số lượng lỗi có thể sửa bởi $SDecode$.

Public key gồm:

1. $H_{pub} = M \cdot H \cdot P \in V_{k \times n}(q)$ là ma trận parity-check của code mới tương đương với code $\mathcal{C}_\lambda$.
2. $t \in \mathbb{N}$ là số lượng lỗi có thể sửa bởi $SDecode$.

#### Thuật toán mã hóa (Enc)

Plaintext được biểu diễn thành vector $m \in V_l(q)$ với $l = \lfloor \log_q ((q - 1)^t \binom{n}{t}) \rfloor$. Ciphertext là vector $c \in V_r(q)$.

Ta cần ánh xạ $\varphi_{n, t, q} : V_l(q) \to V_n(q)$ là đơn ánh, với mỗi $m \in V_l(q)$ cho ra vector $e \in V_n(q)$ có trọng số Hamming là $t$.

1. $e \gets \varphi_{n, t, q}(m)$
2. $c \gets e \cdot H_{pub}^\top$

#### Thuật toán giải mã (Dec)

Đẻ giải mã ta cần ánh xạ $\varphi_{n, t, q}^{-1}$ là ánh xạ ngược của $\varphi_{n, t, q}$.

1. $s \gets M^{-1} c^\top$
2. $e \gets SDecode(c)$
3. $e \gets e \cdot P$
4. $m \gets \varphi^{-1}_{n, t, q}(e)$

