## An Introduction to Mathematical Cryptography

Lời giải cho quyển sách {cite}`Hoffstein2014` của Hoffstein (quyển sách crypto có vẻ là được ... overrated nhất).

Trong phần này, bài giải mình sẽ viết tiếng Việt còn đề bài là tiếng Anh (mình lười nên chép lại từ sách :v).

### Chapter 2. Discrete Logarithms and Diffie-Hellman

**Câu 2.3** Let $g$ be a primitive root of $\mathbb{F}_p$.

(a) Suppose that $x = a$ and $x = b$ are both integer solutions to the congruence $g^x \equiv h$ (mod $p$). Prove that $a \equiv b$ (mod $p-1$). Explain why this implies that the map (2.1) on page 64 is well-defined

(b) Prove that $\log_g(h_1 h_2) = \log_g(h_1) + \log_g(h_2)$ for all $h_1, h_2 \in \mathbb{F}^*_p$

(c) Prove that $\log_g(h^n) = n\log_g(h)$ for all $h \in \mathbb{F}^{*}_p$ and $n \in \mathbb{Z}$

**Giải.** Các tính chất cơ bản của hàm Euler.

(a) Cả $a$ and $b$ là nghiệm của đồng dư $g^x \equiv h$ (mod $p$) nên $g^a \equiv h \pmod p$ và $g^b \equiv h \pmod p$. 
    
Suy ra ta có $g^{-b} \equiv h^{-1} \pmod p$.

Ta nhân kết quả với đồng dư đầu thì được $g^a g^{-b} \equiv h h^{-1} \equiv 1 \pmod p$, hay $g^{a-b} \equiv 1 \pmod p$. 

Do $g$ là primitive root of $\mathbb{F}_p$ tên ta có $\phi(p) \mid (a-b)$, tương đương với $(p-1) \mid (a-b)$.

Như vậy $a - b \equiv 0 \pmod{p-1}$ hay $a \equiv b \pmod {p-1}$ (đpcm).

(b) Giả sử $h_1 \equiv g^{x_1} \pmod p$ và $h_2 \equiv g^{x_2} \pmod p$.

Suy ra $x_1 = \log_g h_1$ và $x_2 = \log_g h_2$ (1).

Do $h_1 h_2 \equiv g^{x_1 + x_2} \pmod p$ nên $x_1 + x_2 = \log_g(h_1 h_2)$ (2).
    
Từ (1) và (2), $\log_g h_1 + \log_g h_2 = \log_g (h_1 h_2)$.
    
(c) tương tự (b).

---

**Câu 2.5** Let $p$ be an odd prime and let $g$ be a primitive root modulo $p$.

Prove that $a$ has a square root modulo $p$ if and only if its discrete logarithm $\log_g(a)$ modulo $p-1$ is even. 

**Giải.** Ta có $g^{p-1} \equiv 1 \pmod p$ do $g$ là primitive root modulo $p$.

**Điều kiện đủ.** Nếu  $a$ là số chính phương modulo $p$ thì tồn tại số $b$ sao cho $b \equiv a^2 \pmod p$.

Suy ra

$$\log_g a = \log_g(b^2) = 2 \log_g b \pmod{p-1},$$

như vậy $\log_ga$ chẵn. 

**Điều kiện cần.** Nếu $\log_g a$ modulo $p-1$ chẵn.

Điều này xảy ra khi

$$\log_ga = 2\log_g b \pmod{p-1}$$

với số $b \in \mathbb{F}_p$ nào đó.

Suy ra

$$\log_ga = \log_g (b^2) \pmod{p-1},$$

hay $a \equiv b^2 \pmod{p-1}$.

Như vậy $a$ có căn bậc hai modulo $p-1$.

---

**Câu 2.10** The exercise describes a public key cryptosystem that requires Bob and Alice to exchange several messages. We illustrate the system with an example.

Bob and Alice fix a publicly known prime $p=32611$, and all of other numbers used are private.

Alice takes her message $m=11111$, chooses a random exponent $a=3589$, and sends the number $u=m^a$ (mod $p$) $=15950$ to Bob.

Bob chooses a random exponent $b=4037$ and sends $v=u^b$ (mod $p$) $=15422$ back to Alice.

Alice then computes $w=v^{15619} \equiv 27257$ (mod $32611$) and sends $w=27257$ to Bob. 

Finally, Bob computes $w^{31883}$ (mod $32611$) and recovers the value $11111$ of Alice's message.

(a) Explain why this algorithm works. In particular, Alice uses the numbers $a=3589$ and 15619 as exponents. How are they related? Similarly, how are Bob's exponents $b=4037$ and 31883 related?

(b) Formulate a general version of this cryptosystem, i.e., using variables, and show how it works in general.

(c) What is the disadvantage of this cryptosystem over Elgamal? (*Hint.* How many times must Alice and Bob exchange data?)

(d) Are there any advantages of this cryptosystem over Elgamal? In particular, can Eve break it if she can solve the discrete logarithm problem? Can Eve break it if she can solve the Diffie-Hellman problem?

**Giải.** 

(a) Ta có

$$3589 \cdot 15619 \equiv 4073 \cdot 31883 \equiv 1 \pmod{p-1}.$$

(b) Alice chọn $a$ và $a'$ sao cho $aa' \equiv 1 \pmod{p-1}$.

Tương tự, Bob chọn $b$ và $b'$ sao cho $bb' \equiv 1 \pmod{p-1}$.

Do đó ta có $aa' = k(p-1)+1$ và $bb' = l(p-1) + 1$.

$$\begin{align*}
    & \Rightarrow v \equiv u^b \equiv (m^a)^b \equiv m^{ab} \pmod p \\
    & \Rightarrow w \equiv v^{a'} \equiv (m^{ab})^{a'} \equiv m^{aa'b} \pmod p \\
    & \Rightarrow w^{b'} \equiv m^{aa'bb'} \equiv m^{[k(p-1)+1]x[l(p-1)+1]} \equiv m^{D(p-1)+1} \equiv m \pmod p.
\end{align*}$$

---

**Câu 2.11** The group $S_3$ consists of the following six distinct elements

$$\begin{equation*}
    e, \sigma, \sigma^2, \tau, \sigma\tau, \sigma^2\tau
\end{equation*}$$

where $e$ is the identity element and multiplication is performed using the rules

$$\begin{equation*}
    \sigma^3 = e, \quad \tau^2 = e, \quad \tau\sigma = \sigma^2\tau
\end{equation*}$$

Compute the following values in the group $S_3$:

(a)  $\tau\sigma^2$

(b)  $\tau(\sigma\tau)$ 

(c)  $(\sigma\tau)(\sigma\tau)$ 

(d)  $(\sigma\tau)(\sigma^2\tau)$

Is $S_3$ a commutative group?


**Giải.**

(a) 

$$\tau\sigma^2 = \tau\sigma\sigma = \sigma^2\tau\sigma = \sigma\sigma^2\tau = \sigma^3\tau = e\tau = \tau$$

(b) 

$$\tau(\sigma\tau)=(\tau\sigma)\tau = \sigma^2\tau\tau = \sigma^2\tau^2 = \sigma^2e = \sigma^2$$

(c) 

$$(\sigma\tau)(\sigma\tau) = \sigma(\tau\sigma)\tau=\sigma(\sigma^2\tau)\tau=\sigma^3\tau^2=ee=e$$

(d) 

$$(\sigma\tau)(\sigma^2\tau)=(\sigma\tau)(\tau\sigma)=\sigma\tau^2\sigma=\sigma e \sigma = \sigma^2$$

$S_3$ không là nhóm giao hoán vì:

$$\sigma\tau = \sigma\tau, \quad \tau\sigma = \sigma^2\tau,$$

đây là hai phần tử phân biệt trong $S_3$.

---

**Câu 2.12** Let $G$ be a group, let $d \geqslant 1$ be an integer, and define a subset of $G$ by

$$\begin{equation*}
    G[d] = \{g \in G: g^d = e\}
\end{equation*}$$

(a) Prove that if $g$ is in $G[d]$, then $g^{-1}$ is in $G[d]$

(b) Suppose that $G$ is commutative. Prove that is $g_1$ and $g_2$ are in $G[d]$, then their product $g_1 \star g_2$ is in $G[d]$

(c) Deduce that if $G$ is commutative, then $G[d]$ is a group.

(d) Show by an example that is $G$ is not a commutative group, then $G[d]$ need not be a group. (*Hint.* Use Exercise 2.11.)


**Giải.**

(a) Vì $g \star g^{-1} = e$ nên 

$$\begin{align*}
    & g \star e \star g^{-1} = e \\
    \Rightarrow & g \star g \star g^{-1} \star g^{-1} = e \\
    \Rightarrow & g^2 \star (g^{-1})^2 = e.
\end{align*}$$

Thực hiện thêm $d-2$ lần nữa và ta nhận được

$$\begin{align*}
    & g^d \star (g^{-1})^d = e \\
    \Rightarrow & e \star (g^{-1})^2 = e \\ 
    \Rightarrow & (g^{-1})^2 = e \\
    \Rightarrow & g^{-1} \in G[d]
\end{align*}$$

(b) Ta có $g_1^d = e$ and $g_2^d = e$. 

Do $G$ là nhóm hoán vị nên $g_1^d \star g_2^d = (g_1 \star g_2)^d$.

Suy ra $(g_1 \star g_2)^d = e \star e = e$.

Như vậy $g_1 \star g_2 \in G[d]$.

(c) Từ câu (b), ta có với mọi $g_1, g_2 \in G[d]$, thì $g_1 \star g_2 \in G[d]$.

Do $e$ là phần tử đơn vị của $G$ nên cũng là phần tử đơn vị của $G[d]$.

Từ câu (a) ta chứng minh được sự tồn tại của phần tử nghịch đảo.

Với $a, b, c \in G[d]$ thì $a^d = b^d = c^d = e$.

Ta có $b^d \star c^d = (b \star c)^d$ do tính giao hoán, suy ra

$$\begin{align*}
    a^d \star (b^d \star c^d) & = a^d \star (b \star c)^d = (a \star b \star c)^d \\
    & = (a \star b)^d \star c^d = (a^d \star b^d) \star c^d.
\end{align*}$$

Như vậy ta chứng minh được tính kết hợp. Và từ đó $G[d]$ là nhóm.

(d) Sử dụng kết quả câu 2.11

$$S_3[2] = \{\tau, \sigma\tau, \sigma^2, \tau, e \}.$$

Vì

$$(\sigma\tau)\tau = \sigma\tau^2 = \sigma \notin S_3[2]$$

nên $S_3[2]$ không là nhóm. 

---

**Câu 2.13** Let $G$ and $H$ be groups. A function $\phi: G \rightarrow H$ is called a (*group*) *homomorphism* if it satisfies

$$\phi(g_1 \star g_2) = \phi(g_1) \star \phi(g_2) \quad \text{for all} \ g_1, g_2 \in G$$

(Note that the product $g_1 \star g_2$ uses the group law in the group $G$, while the product $\phi(g_1) \star \phi(g_2)$ uses the group law in the group $H$.)

(a) Let $e_G$ be the identity element of $G$, let $e_H$ be identity element of $H$, and the $g \in G$. Prove that

$$\phi(e_G) = e_H \quad\quad \text{and} \quad\quad \phi(g^{-1}) = \phi(g)^{-1}$$

(b) Let $G$ be a commutative group. Prove that the map $\phi: G \rightarrow G$ defined by $\phi(g)=g^2$ is a homomorphism. Give an example of a noncommutative group for which this map is not a homomorphism.

(c) Same question as (b) for the map $\phi(g)=g^{-1}$.


**Giải.**

(a) Với mọi $g \in G$ thì $g = g \star e = e \star g$. Suy ra

$$\begin{align*}
    & \phi(g) = \phi(g \star e_G) = \phi(e_G \star g) \\
    \Longleftrightarrow \ & \phi(g) = \phi(g) \star \phi(e_G) = \phi(e_G) \star \phi(g)
\end{align*}$$

Do $\phi(g) \in H$, $\phi(e_G)$ là phần tử đơn vị của $H$, nói cách khác là $\phi(e_G) = e_H$.

Trong nhóm $G$, $g \star g^{-1} = e_G$. Suy ra

$$\begin{align*}
    & \phi(g \star g^{-1}) = \phi(e_G) \\
    \Longleftrightarrow \ & \phi(g) \star \phi(g^{-1}) = \phi(e_G) \\
    \Longleftrightarrow \ & \phi(g) \star \phi(g^{-1}) = e_H \\
    \Longleftrightarrow \ & \phi(g^{-1}) = \phi(g)^{-1}
\end{align*}$$

(b) $\phi: G \rightarrow G$, $\phi(g) = g^2$. Với mọi $g_1, g_2 \in G$, do $G$ là nhóm giao hoán nên

$$\phi(g_1 \star g_2) = (g_1 \star g_2)^2 = g_1^2 \star g_2^2$$

Ta có $g_1^2 \star g_2^2 = \phi(g_1) \star \phi(g_2)$ nên $\phi(g_1 \star g_2) = \phi(g_1) \star \phi(g_2)$. Như vậy $G$ là homomorphism.

Xét nhóm ở Câu 2.11 và ánh xạ $\phi: G \rightarrow G$, $\phi(g)=g^2$.

Khi đó

$$\begin{align*}
    \phi(e) = e^2 = e, & \quad \phi(\sigma) = \sigma^2, \\
    \phi(\tau) = \tau^2 = e, & \quad \phi(\sigma\tau) = (\sigma\tau)^2 = e.
\end{align*}$$

Vì

$$\phi(\sigma\tau) = e \neq \sigma^2 = \phi(\sigma)\phi(\tau),$$

nên $G$ không là homomorphism.

(c) $\phi: G \rightarrow G$, $\phi(g) = g^{-1}$.

Với mọi $g_1, g_2 \in G$ thì $g_1 g_1^{-1} = e$ và $g_2 g_2^{-1} = e$

Do đó $g_1 g_1^{-1} g_2 g_2^{-1} = e$, mà $G$ là nhóm hoán vị nên $(g_1 g_2)(g_1^{-1} g_2^{-1}) = e$, tương đương với $g_1^{-1} g_2^{-1} = (g_1 g_2)^{-1}$. Như vậy

$$\phi(g_1 g_2) = (g_1 g_2)^{-1} = g_1^{-1} g_2^{-1} = \phi(g_1) \phi(g_2)$$

Kết luận: $G$ là homomorphism.

Xét nhóm ở Câu 2.11 và ánh xạ $\phi: G \rightarrow G$, $\phi(g) = g^{-1}$. Ta có

$$\begin{align*}
    \sigma\sigma^2 = e = \sigma^2\sigma = e, \quad \tau^2 = e, \quad (\sigma\tau)^2 = e, \quad (\sigma^2\tau)^2 = e.
\end{align*}
$$

Suy ra

$$\phi(\sigma\tau) = \sigma\tau, \quad \phi(\sigma) = \sigma^2, \quad \phi(\tau) = \tau$$

Vì $\phi(\sigma\tau) = \sigma\tau \neq \sigma^2\tau = \phi(\sigma)\phi(\tau)$ nên $G$ không là homomorphism.

---

**Câu 2.14.** Prove that each of the following maps is a group homomophism.

(a) The map $\phi: \mathbb{Z} \rightarrow \mathbb{Z}/N\mathbb{Z}$ that sends $a \in Z$ to $a$ mod $N$ in $\mathbb{Z}/N\mathbb{Z}$.

(b) The map $\phi: \mathbb{R}^* \to GL_2(\mathbb{R})$ defined by $\phi(a) = \begin{pmatrix}a & 0 \\ 0 & a^{-1}\end{pmatrix}$.

(c) The discrete logarithm map $\log_g: \mathbb{F}_p^* \rightarrow \mathbb{Z}/(p-1)\mathbb{Z}$, where $g$ is a primitive root modulo $p$.

**Giải.**

(a) Với mọi $a, b \in \mathbb{Z}$, 

$$\begin{align*}
    \phi(ab) & = (ab) \pmod N \\
    & = (a \bmod N) \ (b \bmod N) \pmod N \\
    & = \phi(a) \phi(b) \\ 
\end{align*}$$

Do đó $\phi$ là homomorphism.

(b) Với mọi $a, b \in \mathbb{R}^*$ thì

$$\phi(ab)=\begin{pmatrix}ab & 0 \\ 0 & (ab)^{-1}\end{pmatrix}$$

Ta có

$$\begin{equation*}
    \phi(a)\phi(b) = \begin{pmatrix}a & 0 \\ 0 & a^{-1}\end{pmatrix}
    \begin{pmatrix}b & 0 \\ 0 & b^{-1}\end{pmatrix} = 
    \begin{pmatrix}ab & 0 \\ 0 & a^{-1}b^{-1}\end{pmatrix}
\end{equation*}$$

Trong $\mathbb{R}^*$ ta có tính chất $(ab)^{-1} = a^{-1}b^{-1}$, do đó $\phi(ab) = \phi(a)\phi(b)$. Suy ra $\phi$ là homomorphism.

(c) Ta chọn ánh xạ $\phi(a) = x$ thỏa mãn $g^x \equiv a \pmod p$.

Khi đó, với mọi $a, b \in \mathbb{F}_p^*$, $\phi(a) = x$, hay $g^x \equiv a \pmod p$, và $\phi(b) = y$, hay $g^y \equiv b \pmod p$.

Ta có $\phi(a) \phi(b) = x+y$ vì $x$, $y \in \mathbb{Z}/(p-1)\mathbb{Z}$, đây là phép cộng trong modulo $p-1$.

Ta lại có $g^{x+y} \equiv ab \pmod p$, suy ra $\phi(ab) = x + y$. Như vậy $\phi(a)\phi(b) = \phi(ab)$ và $\phi$ là homomorphism.

---

**Câu 2.15.**

(a) Prove that $\text{GL}_2(\mathbb{F}_p)$ is a group.

(b) Show that $GL_2(\mathbb{F}_p)$ is a noncommutative group for every prime $p$.

(c) Describe $GL_2(\mathbb{F}_p)$ completely. That is, list its elements and describe the multiplication table.

(d) How many elements are there in the group $GL_2(\mathbb{F}_p)$?

(e) How many elements are there in the group $GL_n(\mathbb{F}_p)$?

**Giải.**

(a) Nếu $A$ và $B$ là hai ma trận thuộc $GL_2(\mathbb{F}_p)$ thì $AB$ cũng thuộc $GL_2(\mathbb{F}_p)$ do $\det(AB) = \det(A) \cdot \det(B)$ khác $0$.

Phần tử đơn vị là $E = \begin{pmatrix}1 & 0\\0 & 1\end{pmatrix}$.

Với mọi $A \in GL_2(\mathbb{F}_p)$, do $\det A \neq 0$ nên luôn tồn tại nghịch đảo của $A$ trong $GL_2(\mathbb{F}_p)$.

Với mọi $A, B, C \in GL_2(\mathbb{F}_p)$ ta đều có $(AB)C=A(BC)$ vì phép nhân ma trận có tính kết hợp.

Kết luận: $GL_2(\mathbb{F}_p)$ là nhóm.

Giả sử ta có $A = \begin{pmatrix}a_{11} & a_{12} \\ a_{21} & a_{22}\end{pmatrix}$ và $B=\begin{pmatrix}b_{11} & b_{12} \\ b_{21} & b_{22}\end{pmatrix}$ với $A, B \in GL_2(\mathbb{F}_p)$.

Phần tử ở hàng $1$ và cột $1$ của tích $AB$ là $(a_{11}b_{11}+a_{12}b_{21}) \pmod p$.

Phần tử ở hàng $1$ và cột $1$ của tích $BA$ là $(b_{11}a_{11} + b_{12}a_{21}) \pmod p$.

Nếu ta chọn $a_{12} \not\equiv b_{21}^{-1}a_{21}b_{21} \pmod p$ thì $AB \neq BA$, do đó nhóm không có tính giao hoán.

(c) Ta liệt kê tất cả ma trận:

$$\begin{align*}
    A_1 = \begin{pmatrix}0 & 1\\1 & 0\end{pmatrix}, \quad A_2 = \begin{pmatrix}0 & 1\\1 & 1\end{pmatrix}, \quad A_3 = \begin{pmatrix}1 & 0\\0 & 1\end{pmatrix}, \\
    A_4 = \begin{pmatrix}1 & 0\\1 & 1\end{pmatrix}, \quad A_5 = \begin{pmatrix}1 & 1\\0 & 1\end{pmatrix}, \quad A_6 = \begin{pmatrix}1 & 1\\1 & 0\end{pmatrix}.
\end{align*}$$

Bảng phép nhân sẽ như sau:

| | $A_1$ | $A_2$ | $A_3$ | $A_4$ | $A_5$ | $A_6$ |
| - | - | - | - | - | - | - |
| $A_1$ | $A_3$ | $A_5$ | $A_1$ | $A_6$ | $A_2$ | $A_4$ |
| $A_2$ | $A_4$ | $A_6$ | $A_2$ | $A_5$ | $A_1$ | $A_3$ |
| $A_3$ | $A_1$ | $A_2$ | $A_3$ | $A_4$ | $A_5$ | $A_6$ |
| $A_4$ | $A_2$ | $A_1$ | $A_4$ | $A_3$ | $A_6$ | $A_5$ |
| $A_5$ | $A_6$ | $A_4$ | $A_5$ | $A_2$ | $A_3$ | $A_1$ |
| $A_6$ | $A_5$ | $A_3$ | $A_6$ | $A_1$ | $A_4$ | $A_2$ |

(d) Hàng đầu $\bm{u}_1$ là vector bất kì thuộc $\mathbb{F}_p^2$ ngoại trừ $(0, 0)$. Do đó ta có $p^2-1$ cách chọn.

Hàng thứ hai $\bm{u}_2$ là vector bất kì ngoại trừ một bội của hàng đầu. Do đó ta có $p^2-p$ cách (loại các cách chọn $i \cdot \bm{u}_1$ với $i = 0, 1, \ldots, p-1$).

Kết luận: có $(p^2-1)(p^2-p)$ phần tử trong $GL_2(\mathbb{F}_p)$.

(e) Tương tự (d), ta chọn hàng đầu $\bm{u}_1$ là bất kì vector nào ngoại từ $(0,0)$. Ta có $p^n-1$ cách chọn.

Hàng thứ hai $\bm{u}_2$ là bất kì vector nào ngoại trừ bội của hàng đầu, nghĩa là loại các tổ hợp $i \cdot \bm{u}_1$ với $i = 0, 1, \ldots, p-1$. Ta có $p^n-p$ cách chọn.

Hàng thứ ba $\bm{u}_3$ là bất kì vector nào ngoại trừ các tổ hợp tuyến tính của $\bm{u}_1$ và $\bm{u}_2$. Số lượng tổ hợp tuyến tính $a_1 \cdot \bm{u}_1 + a_2 \cdot \bm{u}_2$ chính là số lượng cặp $(a_1, a_2)$ và ta có $p^2$ trường hợp (vì $a_1, a_2 \in \mathbb{F}_p$). Như vậy hàng thứ ba có $p^n-p^2$ cách chọn.

Tổng quát, vector thứ $n$ (hàng thứ $n$) là bất kì vector nào ngoại trừ tổ hợp tuyến tính của các vector trước đó $\bm{u}_1$, $\bm{u}_2$, ..., $\bm{u}_{n-1}$. Như vậy ta có $p^n-p^{n-1}$ cách chọn.

Kết luận: có tất cả $(p^n-1)(p^n-p) \cdots (p^n-p^{n-1})$ phần tử trong $GL_n(\mathbb{F}_p)$.

---

**Câu 2.18.** Solve each of the following simultaneous systems of congruences (or explain why no solutions exists).

(a) $x \equiv 3 \pmod 7$ and $x \equiv 4 \pmod 9$

(b) $x \equiv 137 \pmod {423}$ and $x \equiv 87 \pmod {191}$

(d) $x \equiv 5 \pmod 9$, $x \equiv 6 \pmod {10}$ and $x \equiv 7 \pmod {11}$

(e) $x \equiv 37 \pmod {43}$, $x \equiv 22 \pmod {49}$ and $x \equiv 18 \pmod {71}$

**Giải.**

(a) Vì $N = 7 \cdot 9 = 63$, đặt $T_1 = 63/7 = 9$, $T_1^{-1} \bmod 7 = 4$, $T_2 = 63/9 = 7$, $T_2^{-1} \bmod 9 = 4$.

$$\Rightarrow x \equiv 3 \cdot 9 \cdot 4 + 4 \cdot 7 \cdot 4 \equiv 220 \equiv 31 \pmod {63}$$

(b) Vì $N=423 \cdot 191=90793$, đặt $T_1=N/423=191$, $T_1^{-1} \bmod 423 = 392$, $T_2=N/191=423$, $T_2^{-1} \bmod 191 = 14$.

$$\Rightarrow x \equiv 137 \cdot 191 \cdot 392 + 87 \cdot 423 \cdot 14 \equiv 27209 \pmod N$$

(c) Không thể tính vì $\gcd(451, 697) = 41 \neq 1$.

(d) Vì $N=9 \cdot 10 \cdot 11 = 990$, đặt $T_1=N/9=110$, $T_1^{-1} \bmod 9 = 5$, $T_2=N/10=99$, $T_2^{-1} \bmod 10=9$, $T_3=N/11=90$, $T_3^{-1} \bmod 11 = 6$

$$\Rightarrow x \equiv 5 \cdot 110 \cdot 5 + 6 \cdot 99 \cdot 9 + 7 \cdot 90 \cdot 6 \equiv 986 \pmod N$$

(e) Vì $N=43 \cdot 49 \cdot 71=149597$, đặt $T_1=N/43=3479$, $T_1^{-1} \bmod 43 = 32$, $T_2=N/49=3053$, $T_2^{-1} \bmod 49=36$, $T_3=N/71=2107$, $T_3^{-1} \bmod 71 = 37$

$$\Rightarrow x \equiv 37 \cdot 3479 \cdot 32 + 22 \cdot 3053 \cdot 36 + 18 \cdot 2107 \cdot 37 \equiv 11733 \pmod N$$

---

**Câu 2.19.** Solve the 1700-year-old Chinese remainder problem from the *Sun Tzu Suan Ching* stated on page 84.

$$\begin{cases}
    x \equiv 2 \pmod 3 \\
    x \equiv 3 \pmod 5 \\
    x \equiv 2 \pmod 7
\end{cases},$$

$\Rightarrow x \equiv 23 \pmod {105}$.

---

**Câu 2.21.**

(a) Let $a,b,c$ be positive integers and suppose that

$$\begin{equation*}
    a \mid c, \quad b \mid c, \quad \text{and} \quad \gcd(a,b)=1
\end{equation*}$$

Prove that $ab \mid c$

(b) Let $x=c$ and $x=c'$ be two solutions to the system of simultaneous congruences in the Chinese remainder theorem. Prove that

$$\begin{equation*}
    c \equiv c' \pmod{m_1m_2...m_k}
\end{equation*}$$

**Giải.**

(a) Do $a \mid c$ nên tồn tại $k \in \mathbb{Z}$ sao cho $c = ka$.

Do $b \mid c$ nên tồn tại $l \in \mathbb{Z}$ sao cho $c = lb$.

Như vậy $ka = lb$. 

Tuy nhiên do $\gcd(a,b) = 1$ nên $a \mid l$, hay $l = ma$ với $m \in \mathbb{Z}$

Như vậy $c=lb=lma$, hay $ab \mid c$.

(b) Nếu $c \equiv c' (\equiv a_i) \pmod m_i$ thì $c \equiv c' \pmod{m_1 m_2 \cdots m_k}$.

---

**Câu 2.23.** Find square roots modulo the following composite moduli

**Giải.**

(a) 215

(b) 2654

(c) 1712, 2477, 3187, 1002

(d) $(\pm 1 \cdot 317 \cdot 1 \pm 1 \cdot 124 \cdot 3 \pm 10 \cdot 28 \cdot 10) \pmod{868}$

---

**Câu 2.24.** Let $p$ be an odd prime, let $a$ be an integer that is not divisible by $p$, and let $b$ is a square root of $a$ modulo $p$. This exercise investigates the square root of $a$ modulo powers of $p$

(a) Prove that for some choise of $k$, the number $b+kp$ is a square root of $a$ modulo $p^2$, i.e., $(b+kp)^2 \equiv a \pmod{p^2}$

(b) The number $b=537$ is a square root of $a=476$ modulo the prime $p=1291$. Use the idea in (a) to compute a square root of 476 modulo $p^2$

(c) Suppose that $b$ is a square root of $a$ modulo $p^n$. Prove that for some choice of $j$, the number $b+jp^n$ is a square root of $a$ modulo $p^{n+1}$

(d) Explain why (c) implies the following statements: If $p$ is an odd prime and if $a$ has a square root modulo $p$, then $a$ has a square root modulo $p^n$ for every power of $p$. Is this true if $p=2$?

(e) Use the method in (c) to compute the square root of 3 modulo $13^3$, given that $9^2\equiv 3 \pmod{13}$

**Giải.**

(a) Đặt $f(b_n)=b_n^2-a \pmod{p^n}$ với $b_1 = b$. Suy ra $f(b_1) = b^2-a \equiv 0 \pmod p$.

Ta cần tìm $b_2$ thỏa $f(b_2)=b_2^2-a \equiv 0 \pmod{p^2}$.

Nói cách khác, $b_2 = b_1 + kp$ nên suy ra

$$f(b_1 + kp) = (b_1 + kp)^2 - a = b_1^2 + 2 b_1 kp + (kp)^2 - a \equiv 0 \pmod{p^2}$$

Tương đương với

$$2b_1k \equiv -(b_1^2-a)/p \pmod{p^2},$$

vì $b_1^2-a \equiv 0 \pmod p$.

Do $2b_1 \not\equiv 0 \pmod{p^2}$ nên tồn tại $k$ thỏa mãn đẳng thức.

(b) Ta có công thức

$$k=-(b^2-a)/p \times (2b)^{-1} \pmod{p^2}$$

(c) Ta chứng minh theo quy nạp với mọi $n \geqslant 1$, tồn tại $b_n \in \mathbb{Z}$ sao cho

$$\begin{align*}
    f(b_n) & = b_n^2-a \equiv 0 \pmod{p^n} \\
    b_n & = b \pmod{p^n}
\end{align*}$$

Trường hợp $n = 1$ là điều kiện ban đầu với $b_1 = b$. Giả sử mệnh đề đúng tới $n$, nghĩa là:

$$\begin{align*}
    f(b_n) & = b_n^2 - a \pmod{p^n} \\
    b_n & = b \pmod{p^n} 
\end{align*}$$

Xét $b_{n+1}$

$$f(b_{n+1})=b_{n+1}^2-a \equiv 0 \pmod{p^{n+1}}.$$

Ta viết $b_{n+1}=b_n+p^nt_n$.

$$\begin{align*}
    \Rightarrow  f(b_{n+1})=b_n^2+2b_np^nt_n+p^{2n}t_n^2 - a \equiv 0 \pmod{p^{n+1}} \\
    \Rightarrow b_n^2+2b_np^nt_n-a \equiv 0 \pmod{p^{n+1}} \ (\text{vì} \ 2n \geqslant n+1) \\
    \Rightarrow 2 b_n t_n \equiv -(b_n^2-a)/p^n \pmod{p^{n+1}} \ \text{từ} \ (2)
\end{align*}$$ 

Nghiệm $t_n$ tồn tại vì ta đã giả sử $2b_n \equiv 0 \pmod{p^{n}}$. Như vậy

$$f(b_{n+1}) \equiv 0 \pmod{p^{n+1}}, \quad \text{và} \quad b_{n+1} \equiv b_n \pmod{p^n}.$$

Chứng minh này dùng cho $b+jp^n$ modulo $p^n$, không phải cho $p^{n+1}$.

(d) Sử dụng quy nạp. Đặc biệt, nếu $p=2$ thì mọi số nguyên đều thỏa.

---

**Câu 2.31** Let $R$ and $S$ be rings. A functions $\phi: R \rightarrow S$ is called a (*ring*) *homomorphism* if it satisfies

$$\phi(a+b)=\phi(a) + \phi(b) \quad \text{and} \quad \phi(a \star b) = \phi(a) \star \phi(b)$$

for all $a, b \in R$.

(a) Let $0_R$, $0_S$, $1_R$ and $1_S$ denote the additive and multiplicative identities of $R$ and $S$, respectively. Prove that

$$\begin{equation*}
    \phi(0_R)=0_S, \, \phi(1_R)=1_S, \, \phi(-a)=-\phi(a), \, \phi(a^{-1})=\phi(a)^{-1}
\end{equation*}$$

where the last equality holds for those $a \in R$ that have a multiplicative inverse.

(b) Let $p$ be a prime, and let $R$ be a ring with the property that $pa = 0$ for every $a \in R$. (Here $pa$ means to add $a$ to itself $p$ times.) Prove that the map 

$$\begin{equation*}
    \phi: R \rightarrow R, \quad \phi(a)=a^p
\end{equation*}$$

is a ring homomorphism. It is called the *Frobenius homomorphism*.

**Giải.** Điều kiện đề bài là $\phi(a+b)=\phi(a)+\phi(b)$ và $\phi(a \star b) = \phi(a) \star \phi(b)$ với mọi $a, b \in R$.

(a) Trong $R$, với mọi $a \in R$ ta có 

$$a+0_R = 0_R+a = a.$$

Suy ra

$$\phi(a)=\phi(a+0_R)=\phi(0_R+a),$$

hay

$$\phi(a)=\phi(a)+\phi(0_R)=\phi(0_R)+\phi(a).$$

Đặt $\phi(a)=b \in S$. Khi đó

$$b=b+\phi(0_R)=\phi(0_R)+b$$

nên suy ra $\phi(0_R)=0_S$.

Trong $R$, với mọi $a \in R$ thì

$$a \star 1_R = 1_R \star a = a.$$

Khi đó

$$\phi(a \star 1_R) = \phi(1_R \star a) = \phi(a)$$

nên suy ra

$$\phi(a) \star \phi(1_R) = \phi(1_R) \star \phi(a) = \phi(a),$$

hay $\phi(1_R) = 1_S$.

Với $\phi(-a) = -\phi(a)$, trong $R$ ta có

$$a + (-a) = (-a) + a = 0_R,$$

suy ra

$$\phi(a+(-a))=\phi((-a)+a)=\phi(0_R),$$

tương đương với

$$\phi(a)+\phi(-a)=\phi(-a)+\phi(a)=\phi(0_R)=0_S.$$

Như vậy $\phi(-a) = -\phi(a)$.

Với $\phi(a^{-1}) = \phi(a)^{-1}$, trong $R$ ta có

$$a \star a^{-1} = a^{-1} \star a = 1_R,$$

suy ra

$$\phi(a \star a^{-1}) = \phi(a^{-1} \star a) = \phi(1_R),$$

tương đương với

$$\phi(a) \star \phi(a^{-1}) = \phi(a^{-1}) \star \phi(a) = \phi(1_R) = 1_S.$$

Như vậy $\phi(a^{-1})=\phi(a)^{-1}$.

(b) Ánh xạ $\phi: R \rightarrow R$ cho bởi $\phi(a)=a^p$, suy ra

$$\displaystyle{\phi(a+b)=(a+b)^p=\sum_{i=0}{p} \binom{p}{i} a^i b^{p-1}}.$$

Vì $p \mid \displaystyle{\binom{p}{i}} = \dfrac{p!}{(p-i)! \cdot i!}$ ($p$ là số nguyên tố) nên suy ra với mọi $1 \leqslant i \leqslant p-1$, ta có $\displaystyle{\binom{p}{i}} = 0$ (do $pa=0$).

$\Rightarrow \phi(a+b)=a^p+b^p=\phi(a)+\phi(b)$ (1)

$\Rightarrow \phi(ab)=(ab)^p=a^p b^p = \phi(a) \phi(b)$ (2)

Từ (1) và (2) ta thu được ring homomorphism.

---

**Câu 2.32.** Prove Proposition 2.41

Vì $a_1 \equiv a_2 \pmod m$ nên $m \mid (a_1 - a_2)$.

Nói cách khác là tồn tại $k \in R$ sao cho $a_1 - a_2 = k \star m$.

Tương tự, tồn tại $l \in R$ sao cho $b_1 - b_2 = l \star m$.

Từ đó

$$a_1 - a_2 + b_1 - b_2 = (k+l) \star m,$$

tương đương với

$$m \mid (a_1 + b_1 - (a_2 + b_2)),$$

hay

$$a_1 + b_1 \equiv a_2 + b_2 \pmod m.$$

Tương tự cho $a_1-b_1 \equiv a_2-b_2 \pmod m$.

Đối với phép nhân, do

$$\begin{equation*}
    \begin{cases}
        a_1 = a_2 + k \star m \\ b_1 = b_2 + l \star m
    \end{cases}
\end{equation*}$$

ta có

$$\begin{align*}
    a_1 \star b_1 & = (a_2 + k \star m)(b_2 + l \star m) \\
    & = a_2 \star b_2 + a_2 \star l \star m + k \star b_2 \star m + k \star l \star m^2
\end{align*}$$

Suy ra $m \mid (a_1 \star b_1 - a_2 \star b_2)$ hay nói cách khác là

$$a_1 \star b_1 \equiv a_2 \star b_2 \pmod m.$$

---

**Câu 2.33.** Prove Proposition 2.43

Theo Câu 2.32, nếu ta có $a' \in \bar{a}$ thì tương đương $a' \equiv a \pmod m$.

Tương tự, nếu ta có $b' \in \bar{b}$ thì tương đương $b' \equiv b \pmod m$.

Như vậy, theo Câu 2.32 thì

$$a' + b' \equiv a+b \pmod m, \quad a' \star b' \equiv a \star b \pmod m$$

Nói cách khác

$$a'+b' \in \overline{a+b} \quad \text{và} \quad a' \star b' \in \overline{a \star b},$$

nói cách khác phép tính cộng và nhân đóng trên $R$ (closed).

Với mọi $a \in R$ ta có

$$\overline{a} + \overline{0} = \overline{a+0} = \overline{a} = \overline{0+a} = \overline{0} + \overline{a}$$

Như vậy phần tử trung hòa của phép cộng là $\overline{0}$.

Với mọi $a \in R$ thì

$$\overline{a} + \overline{m-a} = \overline{a + m - a} = \overline{0} = \overline{m-a} + \overline{a},$$

suy ra $\overline{m-a}$ là phần tử đối của phần tử $a$ trong phép cộng.

Phép cộng trong modulo cũng có tính kết hợp

$$\overline{a} + (\overline{b}+\overline{c}) = \overline{a} + \overline{b+c} = \overline{a+b+c} = \overline{a+b} + \overline{c} = (\overline{a}+\overline{b})+\overline{c}$$

Với mọi $a, b \in R$

$$\overline{a}+\overline{b}=\overline{a+b}=\overline{b+a}=\overline{b}+\overline{a}$$

nên phép cộng modulo có tính giao hoán.

Vì $a \star 1 \equiv a \pmod m$ với mọi $a \in R$ nên

$$\overline{a} \star \overline{1} = \overline{a \star 1} = \overline{a} = \overline{1 \star a} = \overline{1} \star \overline{a}.$$

Suy ra phần tử đơn vị của phép nhân là $\overline{1}$.

Với mọi $a, b, c \in R$ ta có $a(bc)=(ab)c \pmod m$. Suy ra tính kết hợp của phép nhân

$$\overline{a} \star (\overline{b} \star \overline{c}) = \overline{a} \star \overline{bc} = \overline{abc} = \overline{ab} \star \overline{c} = (\overline{a} \star \overline{b}) \star \overline{c}.$$

Vì

$$\overline{a} \star \overline{b} = \overline{a \star b} = \overline{b \star a} = \overline{b} \star \overline{a}$$

ta có tính giao hoán của phép nhân.

Tính phân phối giữa phép nhân và phép cộng:

$$\overline{a} \star (\overline{b} + \overline{c}) = \overline{a} \star \overline{b + c} = \overline{a(b+c)} = \overline{ab + ac} = \overline{ab} + \overline{ac} = \overline{a} \star \overline{b} + \overline{a} \star \overline{c}.$$

Như vậy, $R/(m)$ là vành (cụ thể vừa là vành với đơn vị vừa là vành giao hoán).

---

**Câu 2.34.** Let $\mathbb{F}$ be a field and let $\mathbf{a}$ and $\mathbf{b}$ be nonzero polynomials in $\mathbb{F}[x]$

(a) Prove that $\deg(\mathbf{a} \cdot \mathbf{b}) = \deg(\mathbf{a}) + \deg(\mathbf{b})$

(b) Prove that $\mathbf{a}$ has a multiplicative inverse in $\mathbb{F}[x]$ if and only if $\mathbb{a}$ is in $\mathbb{F}$, i.e., if and only if $\mathbb{a}$ is a constant polynomial

(c) Prove that every nonzero element of $\mathbb{F}[x]$ can be factored into a product of irreducible polynomials. (*Hint.* Use (a), (b) and induction on the degree of the polynomial.)

(d) Let $R$ be ring $\mathbb{Z}/6\mathbb{Z}$. Give an example to show that (a) is false for some polynomials $\mathbf{a}$ and $\mathbf{b}$ in $R[x]$.

**Giải.**

(a) Đặt

$$\mathbf{a} = a_n x^n + a_{n-1} x^{n-1} + \cdots + a_1 x + a_0,$$

với $a_i \in \mathbb{F}$ và $\deg(\mathbf{a}) = n$.

Đặt

$$b = b_m x^m + b_{m-1} x^{m-1} + \cdots + b_1 x + b_0,$$

với $b_i \in \mathbb{F}$ và $\deg(\mathbf{b}) = m$. 

Hạng tử với bậc cao nhất trong phép nhân $\mathbf{a} \cdot \mathbf{b}$ là $x^{n+m}$, do đó

$$\deg(\mathbf{a} \cdot \mathbf{b}) = n + m = \deg(\mathbf{a}) + \deg(\mathbf{b}).$$

(b) Với

$$\mathbf{a} = a_n x^n + a_{n-1} x^{n-1} + \cdots + a_1 x + a_0$$

Giả sử $\mathbf{a}$ có nghịch đảo trong $\mathbb{F}[x]$ là đa thức

$$\mathbf{b}=b_m x^m + b_{m-1} x^{m-1} + \cdots + b_1 x + b_0.$$

Vì

$$\begin{align*}
    \mathbf{ab} = & \sum_{i=0}^n a_i x_i \sum_{j=0}^m b_j x^j  = \sum_{i=0}^n \sum_{j=0}^m a_i b_j x^{i+j} = 1
\end{align*}$$

Đồng nhất hệ số ta có $a_0 b_0 = 1$, các tích khác bằng $0$. Như vậy $\mathbf{a}$ là đa thức hằng.

(c)

(d) $\mathbf{a} = 2x^2 + 3x + 1$, $\mathbf{b} = 3x + 2$.

Trong $\mathbb{Z}/6\mathbb{Z}$ các hệ số được modulo cho $6$ và ta có

$$\mathbf{a} \mathbf{b} = x^2 + 3x + 2$$

Như vậy $\deg(\mathbf{a} \mathbf{b}) = 2 < 3 = \deg(\mathbf{a}) + \deg(\mathbf{b})$

---

**Câu 2.35**, **Câu 2.36**. Programming on Sagemath

---

**Câu 2.37.** Prove that the polynomial $x^3+x+1$ is irreducible in $\mathbb{F}_2[x]$

**Giải.**

Nếu $f(x) = x^3+x+1$ có nhân tử nào khác $1$ và chính nó thì đa thức đó phải có bậc nhỏ hơn $3$.

Các đa thức như vậy trong $\mathbb{F}_2[x]$ là

$$0, x+1, x^2, x^2+1, x^2+x, x^2+x+1, x.$$

Tuy nhiên $f(x)$ không chia hết cho bất kì đa thức nào kể trên nên $f(x)$ là đa thức tối giản.

---

**Câu 2.38.** Programming on Sagemath

---

**Câu 2.39.** The field $\mathbb{F}_7[x]/(x^2+1)$ is a field with 49 elements, which for the moment we donote by $\mathbb{F}_{49}$

Using example **2.58**, every element in $\mathbb{F}_7[x]/(x^2+1)$ has form $f(x)=a+bx$, so in $\mathbb{F}_{49}$ it has form $a+bi$ (here $i^2=-1$)

(a) Is $2+5x$ is a primitive root in $\mathbb{F}_{49}$? No because $(2+5x)^8=1$

(b) Is $2+x$ is a primitive root in $\mathbb{F}_{49}$? Yes

(c) Is $1+x$ is a primitive root in $\mathbb{F}_{49}$? No because $(1+x)^{24} = 1$

---

**Câu 2.41.** Let $\mathbb{F}$ is a finite field.

(a) Prove that there is an integer $m \geqslant 1$ such that if we add 1 to itself $m$ times,

$$\underbrace{1+1+\cdots+1}_{m \text{ ones}}$$

then we get 0. Note that here 1 and 0 are the multiplicative and additive identity elements of the field $\mathbb{F}$.

<!-- Because 1 is element of $\mathbb{F}$, then $\underbrace{1+1+\cdots+1}_{n \text{ times}}$ always is an element of $\mathbb{F}$. And $\mathbb{F}$ is finite field, so there is $m \geqslant 1$ such that $\underbrace{1+1+\cdots+1}_{m \text{ times}}$ equals to 0 (1, 1+1, 1+1+1, ... cannot all be different) -->

(b) Let $m$ be the smallest positive integer with the property described in (a). Prove that $m$ is prime. This prime is called the *characteristic of the field $\mathbb{F}$*.

<!-- Suppose that $m$ can be factor, so $m=pq$ ($1 < p, q < m$) and then 

$\Rightarrow \underbrace{1+1+\cdots+1}_{m \text{ times}} = 0$. Therefore we can write as \[ \overbrace{\underbrace{(1+1+\cdots+1)}_{p \text{ times}} + \underbrace{(1+1+\cdots+1)}_{p \text{ times}} + \cdots + \underbrace{(1+1+\cdots+1)}_{p \text{ times}}}^{q \text{ times}}\] 

Because $\mathbb{F}$ is a finite field, $\underbrace{1+1+\cdots+1}_{p \text{ times}} = a \in \mathbb{F}$ 

$\Rightarrow q \cdot a = 0$ ($q > 1$ and $a$ cannot be 0 because $m$ is the smallest number that satisfies $1+1+\cdots+1=0$

$\Rightarrow$ contraction $\Rightarrow \mathbb{F}$ cannot be a field.

So $m$ is a prime  -->

### Chapter 3. Integer Factorization and RSA

**Câu 3.4.** *Euler's phi function $\phi(N)$* is the function defined by

$$\phi(N) = | \{0 \leqslant k < N: \gcd(k, N)=1\} |.$$

**Giải.**

Chứng minh định lý Euler đã có trong bài viết về hàm Euler.

---

**Câu 3.5.** Properties of Euler's phi function

If $p$ and $q$ are distinct primes, how is $\phi(pq)$ related to $\phi(p)$ and $\phi(q)$?

**Giải.**

Chứng minh tính chất nhân tính của hàm Euler đã có ở bài viết về hàm Euler.

---

**Câu 3.6.** Let $N$, $c$, and $e$ be positive integers satisfying the conditions $\gcd(N,c)=1$ and $\gcd(e,\phi(N))=1$.

Explain how to solve the congruence $x^e \equiv c \pmod{N}$ assuming that you know the value of $\phi(N)$

**Giải.**

Vì $\gcd(e, \phi(N)) = 1$, ta có thể tìm số $d \in \mathbb{Z}$ sao cho $ed \equiv 1 \pmod{\phi(N)}$ với thuật toán Euclid mở rộng.

Khi đó $ed = k\phi(N) + 1$ với $k \in \mathbb{Z}$.

VÌ $\gcd(N, c)=1$ nên $\gcd(N,x)=1$, hay

$$c^d = \Big(x^e\Big)^d = x^{ed} = x^{k\phi(N) + 1} = (x^k)^{\phi(N)}x,$$

và ta đã biết $(x^k)^{\phi(N)} \equiv 1 \pmod{N}$ từ Câu 3.4.

Như vậy $c^d \equiv x \pmod{N}$.

---

**Câu 3.11.** Alice chooses two large primes $p$ and $q$ and she publishes $N=pq$. It is assumed that $N$ is hard to factor. Alice also chooses three random numbers $g$, $r_1$, and $r_2$ modulo $N$ and computes

$$g_1 \equiv g^{r_1(p-1)} \pmod{N} \qquad \text{and} \qquad g_2 \equiv g^{r_2(q-1)} \pmod{N}$$

Her public key is the triple $(N, g_1, g_2)$ and her private key is the pair of primes $(p, q)$.

Now Bob wants to send the message $m$ to Alice, where $m$ is a number modulo $N$. He chooses two random integers $s_1$ and $s_2$ modulo $N$ and computes

$$c_1 \equiv mg_1^{s_1} \pmod{N} \qquad \text{and} \qquad c_2 \equiv mg_2^{s_2} \pmod{N}$$

Bob sends the ciphertext $(c_1, c_2)$ to Alice.

Decryption is extreamly fast and essy. Alice uses the Chinese remainder theorem to solve the pair of congruences

$$x \equiv c_2 \pmod{p} \qquad \text{and} \qquad x \equiv c_2 \pmod{q}$$
    
Prove that Alice's solution $x$ is equal to Bob's plaintext $m$.

**Giải.**

Ta có

$$c_1 \equiv mg_1^{s_1} \pmod{N} \equiv mg_1^{s_1} \pmod{p} \equiv m \pmod{p}$$

do $g_1^{s_1} = (g_1^{s_1 r_1})^{(p-1)} \equiv 1 \pmod{p}$.

Tương tự ta có $c_2 \equiv m \pmod{q}$.

Nghiệm của hệ đồng dư là

$$x \equiv c_1 q q' + c_2 p p' \pmod N$$

với $p p' + q q' = 1$.

$\Rightarrow x \equiv m p p' + m q q' \equiv m(p p' + q q') \equiv m \pmod N$
        
Ta có

$$g_1 \equiv g^{r_1 (p-1)} \pmod N \equiv g^{r_1 (p-1)} \pmod p \equiv 1 \pmod p.$$

Suy ra $p = \gcd(g_1-1, N)$. Tương tự, $q = \gcd(g_2-1, N)$.

Như vậy ta đã khôi phục lại private key.

---

**Câu 3.13.** Find $x$, $y$ such that $xe_1 + ye_2=1=\gcd(e_1,e_2)$

$$\Rightarrow m=c_1^x c_2^y = m^{e_1 x + e_2 y} = m \pmod{N}$$

---

<!-- **Câu 3.14.** Because 3, 11 and 17 are primes number, $a \equiv a^3 \pmod 3$, $a \equiv a^{11} \pmod{11}$, $a \equiv a^{17} \pmod{17}$. We have system congruence

$$\begin{align*}
    a & \equiv a^3 \pmod 3 \\ a & \equiv a^{11} \pmod{11} \\ a & \equiv a^{17} \pmod{17}
\end{align*}$$

Consider that $a^3 \equiv a \pmod 3$, $a^{3^2} \equiv a^3 \equiv a \pmod 3$, $\cdots$, $a^{3^i} \equiv a \pmod 3$. And $561 = 2 \cdot 3^5 + 2 \cdot 3^3 + 2 \cdot 3^2 + 3^1$, $a^{561} \equiv a^2 \cdot a^2 \cdot a^2 \cdot a \equiv a^9 \equiv a \pmod 3$.

Similarly, $a^{561} \equiv a \pmod{11}$, $a^{561} \equiv a \pmod{17}$. From system congruence:

$$\begin{align*}
    a^{561} & \equiv a \pmod 3 \\ a^{561} & \equiv a \pmod{11} \\ a^{561} & \equiv a \pmod{17}
\end{align*}$$

Using CRT, $a^{561} = (187 \cdot 1 \cdot a + 51 \cdot 8 \cdot a + 33 \cdot 16 \cdot a) \pmod{561} = a \pmod{561}$

Suppose that $n$ is even ($n \geqslant 4$), we have 

$$(n-1)^{n-1} = (-1)^{n-1} = -1 \pmod n,$$

but $a^{n-1} \equiv 1 \pmod n$ for all $a$, which is contrary. So $n$ must be odd.
Suppose that $n = p_1^{e_1} p_2^{e_2} \cdots p_r^{e_r}$ ($p_i$ is odd prime). Because $a^{p^{e-1} (p-1)} \equiv 1 \pmod{p^e}$ and $a^{n-1} \equiv 1 \pmod n$, we have $a^{n-1} \equiv 1 \pmod{p^e}$.

$\Rightarrow p^{e-1}(p-1) \mid (n-1) \Rightarrow p^{e-1} \mid (n-1)$, but $p^{e-1} \mid n$, which is contrary if $e \geqslant 2$. Hence $e$ must be 1.

So $n = p_1 p_2 \cdots p_r$ -->
    
---

<!-- **Câu 3.37.**

$$\Big(a^{\frac{p-1}{2}}\Big)^2 \equiv a^{p-1} \equiv 1 \pmod p$$

$\Rightarrow \binom{a}{p} = \pm 1$

$\Rightarrow \Big(a^{\frac{p-1}{2}} - 1\Big)\Big(a^{\frac{p-1}{2}} + 1\Big) \equiv 0 \pmod p$

$\Rightarrow a^{\frac{p-1}{2}} \equiv \pm 1 \pmod p$
    
If $a$ is quadratic residue, then $a \equiv b^2 \pmod p$ 

$\Rightarrow a^{\frac{p-1}{2}} \equiv (b^2)^{\frac{p-1}{2}} = b^{p-1} \equiv 1 \pmod p$

If $a^{\frac{p-1}{2}} \equiv 1 \pmod p$

Let $g$ be generator modulo $p$, then $a \equiv g^m \pmod p$

If $m$ is even $\Rightarrow a \equiv g^{2k} \pmod p \Rightarrow a^{\frac{p-1}{2}} \equiv 1 \pmod p$

If $m$ is odd $\Rightarrow a = g^{2k+1} \pmod p \Rightarrow a^{\frac{p-1}{2}} \equiv g^{(2k+1)\frac{p-1}{2}} \equiv g^{p-1} g^{\frac{p-1}{2}} \equiv g^{\frac{p-1}{2}}\not\equiv 1 \pmod p$, because $p-1$ is smallest number that $g^{p-1} \equiv 1 \pmod p$

From (a) and (b) $\binom{-1}{p} \equiv (-1)^{\frac{p-1}{2}} \pmod p$, if $p=4k+1 \Rightarrow (-1)^{\frac{p-1}{2}} \equiv (-1)^{2k} \equiv 1 \pmod p$ \\ If $p=4k+3 \Rightarrow (-1)^{\frac{p-1}{2}} \equiv (-1)^{2k+1} \equiv -1 \pmod p$ -->

---

**Câu 3.38.** Prove that the three parts of the quadratic reciprocity theorem are equivalent to the following three concise formulas, where $p$ and $q$ are odd primes.

<!-- $\Big(\frac{-1}{p}\Big) = (-1)^{\frac{p-1}{2}}$

With $p \equiv 1 \pmod 4 \Rightarrow \Big(\frac{-1}{p}\Big) = 1 = (-1)^{\frac{p-1}{2}} \pmod p$ \\ Similarly with $p \equiv 3 \pmod 4$
    $\Big(\frac{2}{p}\Big) = (-1)^{\frac{p^2-1}{8}}$

First we need a lemma (**Gauss lemma**): suppose $p$ is an odd prime, and $a \in \mathbb{Z}$, $\gcd(a, p) = 1$. Consider the set
\[a, 2a, 3a, \cdots, \frac{p-1}{2}a\]

If $s$ of those residues are greater than $\frac{p}{2}$, then $\binom{a}{p} = (-1)^s$

\underline{Proof of lemma}: Among smallest residues of 
\[a, 2a, 3a, \cdots, \frac{p-1}{2}a\], suppose that 
\[u_1, u_2, \cdots, u_s\] are residues greater than $\frac{p}{2}$, and 
\[v_1, v_2, \cdots, v_t\] are residues smaller than $\frac{p}{2}$

Because $\gcd(ja, p)=1 \forall j, 1 \leqslant j \leqslant \frac{p-1}{2}$, all $u_i, v_j \neq 0 \Leftrightarrow u_i, v_j \in \{1,2,\cdots,p-1\}$. We will prove that, the set 
\[\{p-u_1, p-u_2, \cdots, p-u_s, v_1, v_2, \cdots, v_t\}\] 
is a permutation of $\{1,2,\cdots,\frac{p-1}{2}\}$

It is clear that there are no 2 numbers $u_i$ or 2 numbers $v_j$ simultaneously congruent modulo $p$. Because if $ma \equiv na \pmod p$ and $\gcd(a,p)=1$, then $m\equiv n \pmod p \Rightarrow$ contrast with $m,n \leqslant \frac{p-1}{2}$

Similarly, we see that there are no numbers $p-u_i$ congruent with $v_j$, so $$\Rightarrow (p-u_1)(p-u_2)\cdots(p-u_s)v_1 v_2 \cdots v_t \equiv \Big(\frac{p-1}{2}\Big)! \pmod p$$

On the other hand, 
\[u_1,u_2,\cdots,u_s, v_1, v_2, \cdots, v_t\] 
are smallest residues of 
\[a, 2a, 3a, \cdots, \frac{p-1}{2}\], so 
\[\Rightarrow u_1 u_2 \cdots u_s v_1 v_2 \cdots v_t \equiv a^{\frac{p-1}{2}} \Big(\frac{p-1}{2}\Big)! \pmod p\]

So $(-1)^s a^{\frac{p-1}{2}} \Big(\frac{p-1}{2}\Big)! \equiv \Big(\frac{p-1}{2}\Big)! \pmod p$

And because $\gcd(p, \Big(\frac{p-1}{2}\Big)!) = 1 \Rightarrow (-1)^s a^{\frac{p-1}{2}} \equiv 1 \pmod p$

$\Rightarrow a^{\frac{p-1}{2}} \equiv (-1)^s \pmod p$ and $\binom{a}{p} = a^{\frac{p-1}{2}}$

$\Rightarrow \binom{a}{p} = (-1)^s \pmod p$

\underline{Return to problem}: using theorem above, we need to find the number of residues, which are greater than $\frac{p}{2}$ among $1 \cdot 2$, $2 \cdot 2$, $\cdots$, $\frac{p-1}{2} \cdot 2$. Therefore we only need to know which numbers are greater than $\frac{p}{2}$

$\Rightarrow$ there are $s = \frac{p-1}{2} - \Big[\frac{p}{4}\Big] \Rightarrow \Big(\frac{2}{p}\Big) = (-1)^{\frac{p-1}{2} - \Big[\frac{p}{4}\Big] }$

With $p \equiv 1, 3, 5, 7 \pmod 8$, we have 
\[\frac{p-1}{2} - \Big[\frac{p}{4}\Big] \equiv \frac{p^2-1}{8} \pmod 2\] 

\[\Rightarrow \Big(\frac{2}{p}\Big) = (-1)^{\frac{p^2-1}{8}}\]

    $\Big(\frac{p}{q}\Big)\Big(\frac{q}{p}\Big) = (-1)^{\frac{p-1}{2} \cdot \frac{q-1}{2}}$

We need a lemma: Suppose $p$ is an odd prime, $a$ is odd and $\gcd(a, p) = 1$, then $\Big(\frac{a}{p}\Big) = (-1)^{T(a, p)}$, with 
\[T(a, p) = \sum_{j=1}^{\frac{p-1}{2}}\Big[\frac{ja}{p}\Big]\]

\underline{Proof of lemma}: consider smallest residues of $a$, $2a$, $3a$, $\cdots$, $\frac{p-1}{2} \cdot a$. As Gauss's lemma, $u_1$, $u_2$, $\cdots$, $u_s$, $v_1$, $v_2$, $\cdots$, $v_t$ are residues greater and less than $\frac{p}{2}$ respectively. According to Euclidean divisor: $$ja = p \Big[\frac{ja}{p}\Big] + \text{remainder}$$, remainder is $u_i$ or $v_j$. We have such $\frac{p-1}{2}$ equations and add them together $$\Rightarrow \sum_{j=1}^{\frac{p-1}{2}}ja = \sum_{j=1}^{\frac{p-1}{2}}p\Big[\frac{ja}{p}\Big] + \sum_{i=1}^{s}u_i + \sum_{j=1}^{t}v_j$$
As we pointed out in Gauss's lemma, the set $p-u_1$, $p-u_2$, $\cdots$, $p-u_s$, $v_1$, $v_2$, $\cdots$, $v_t$ is a permutation of the set 1, 2, $\cdots$, $\frac{p-1}{2}$
$$\sum_{j=1}^{\frac{p-1}{2}}j = \sum_{i=1}^{s}(p-u_i) + \sum_{j=1}^{t}v_t = ps - \sum_{i=1}^{s}u_i + \sum_{j=1}^{t}v_t$$
$$\Rightarrow \sum_{j=1}^{\frac{p-1}{2}}ja - \sum_{j=1}^{\frac{p-1}{2}}j = \sum_{j=1}^{\frac{p-1}{2}}p\Big[\frac{ja}{p}\Big] - ps + 2\sum_{i=1}^{s}u_i$$
From formula of $T(a, p)$, $(a-1)\sum_{j=1}^{\frac{p-1}{2}}j = pT(a, p) - ps + 2 \sum_{i=1}^{s}u_i$

Because $a$, $p$ are odd, $T(a, p) \equiv s \pmod 2$. From Gauss's lemma we finish.

\underline{Return to problem}: Consider pairs $(x, y)$, where $1 \leqslant x \leqslant \frac{p-1}{2}$ and $1 \leqslant y \leqslant \frac{q-1}{2}$, there are $\frac{p-1}{2}\cdot\frac{q-1}{2}$ pairs. We divide those pairs into 2 groups, depending on the magnitude of $px$ and $qy$.

Because $p$, $q$ are two different primes, $px \neq qy$, $\forall (x, y)$

We consider pairs with $qx > py$. With every fixed element of $x$ ($1 \leqslant x \leqslant \frac{p-1}{2}$), exist $\Big[\frac{qx}{p}\Big]$ elements $y$ satisfying $1 \leqslant y \leqslant \frac{qx}{p}$. Therefore, there are $\sum_{i=1}^{\frac{p-1}{2}}\Big[\frac{iq}{p}\Big]$ pairs. When $qx < py$, similarly, there are $\sum_{j=1}^{\frac{q-1}{2}}\Big[\frac{jp}{q}\Big]$ pairs. Because there are $\frac{p-1}{2} \cdot \frac{q-1}{2}$ pairs, we have equation $$\sum_{i=1}^{\frac{p-1}{2}}\Big[\frac{iq}{p}\Big] + \sum_{j=1}^{\frac{q-1}{2}}\Big[\frac{jp}{q}\Big] = \frac{p-1}{2} \cdot \frac{q-1}{2}$$
From definition of $T(p, q)$, we have result $$(-1)^{T(p, q) + T(q, p)} = (-1)^{\frac{p-1}{2} \cdot \frac{q-1}{2}}$$ -->

---

**Câu 3.39.** Let $p$ be a prime satisfying $p \equiv 3 \pmod 4$.

Let $a$ be a quadratic residue modulo $p$. Prove that the number

$$b \equiv a^{\frac{p+1}{4}} \pmod p$$

has the property that $b^2 \equiv a \pmod p$. (*Hint.* Write $\dfrac{p+1}{2}$ as $1+\dfrac{p-1}{2}$ and use Exercise 3.37.) This gives an easy way to take square roots modulo $p$ for primes that are congruent to 3 modulo 4.

**Giải.**

Dùng Câu 3.37, $a^{\frac{p-1}{2}} \equiv 1 \pmod p$ vì $a$ là thặng dư chính phương modulo $p$.

Khi đó

$$b^2 \equiv a^{\frac{p+1}{2}} \equiv a^{1+\frac{p-1}{2}} \equiv a \cdot a^{\frac{p-1}{2}} \equiv a \cdot 1 \equiv 1 \pmod p$$

---

**Câu 3.40.** Let $p$ be and odd prime, let $g \in \mathbb{F}^{*}_p$ be a primitive root, and let $h \in \mathbb{F}^{*}_p$. Write $p - 1 = 2^sm$ with $m$ odd and $s \geqslant 1$, and write the binary expansion of $\log_g(h)$ as

$$log_g(h) = \varepsilon_0 + 2\varepsilon_1 + 4\varepsilon_2 + 8\varepsilon_3 + \cdots \quad \text{with} \quad \varepsilon_0, \varepsilon_1, \cdots \in \{0, 1\}$$

Give an algorithm that generalizes Example 3.69 and allows you to rapidly compute $\varepsilon_0, \varepsilon_1, \cdots, \varepsilon_{s-1}$, thereby proving that the first $s$ bits of the discrete logarithm are insecure.

**Giải.**

````{prf:algorithm} Thuật toán tìm $s$ least significant bit (LSB) của $x$ trong $g^x \equiv h \pmod p$
**Input:** $g$, $h$, $p$ ($p-1=2^s m$)

**Output:** $s$ least significant bits của $x$ trong $g^x \equiv h \pmod p$

1. Ta sẽ tìm mảng $\varepsilon_0, \varepsilon_1, \cdots, \varepsilon_{s-1}$
2. For $i = 0, \ldots, s-1$
    1. If $h$ là thặng dư chính phương
        1. $\varepsilon_i = 0$, $h = \sqrt{h} \pmod p$
    2. ElseIf $\varepsilon_i = 1$
        1. $h = \sqrt{g^{-1}h} \pmod p$
    3. EndIf
3. EndFor
````

---

**Câu 3.41.** Let $p$ be a prime satisfying $p \equiv 1 \pmod 3$. We say that $a$ is a *cubic residue modulo $p$* if $p \nmid a$ and there is an integer $c$ satisfying $a \equiv c^3 \pmod p$.

(a) Let $a$ and $b$ be cubic residues modulo $p$. Prove that $ab$ is a cubic residue modulo $p$.

(b) Give an example to show that (unlike the case with quadratic residues) it is possible for none of $a$, $b$ and $ab$ to the a cubic residue modulo $p$

(c) Let $g$ be a primitive root modulo $p$. Prove that $a$ is a cubic residue modulo $p$ if and only if $3 \mid \log_g(a)$, where $\log_g(a)$ is the discrete logarithm of $a$ to the base $g$.

(d) Suppose instead that $p \equiv 2 \pmod 3$. Prove that for every integer $a$ there is an integerr $c$ satisfying $a \equiv c^3 \pmod p$. In other words, if $p \equiv 2 \pmod 3$, show that every number is a cube modulo $p$.

**Giải.**

(a) Ta có $a \equiv x^3 \pmod p$ và $y \equiv y^3 \pmod p$ với $x$ và $y$ nào đó thuộc $\mathbb{F}_p$.

Suy ra $ab \equiv x^3 y^3 = (xy)^3 \pmod p$ cũng là thặng dư bậc ba.

(b) Gọi $g$ là primitive root modulo $p$.

Ta chọn $a \equiv g^{3k+1} \pmod p$ và $b \equiv g^{3k'+1} \pmod p$.

Khi đó $ab \equiv g^{(3k+1)+(3k'+1)} \equiv g^{3(k+k')+2} \pmod p$ không phải thặng dư bậc ba.

(c)

**Điều kiện đủ**. Nếu $a$ là thặng dư bậc ba modulo $p$, giả sử $a \equiv c^3 \pmod 3$ và $c \equiv g^u = \pmod p$.

Khi đó $a = g^{3u} \pmod p$ và theo định lý Lagrange thì $3 \mid \log_g(a)$.

**Điều kiện cần.** Nếu $3 \mid \log_g(a)$ thì làm ngược lại bước chứng minh điều kiện đủ.


(d) Vì $p \equiv 2 \pmod 3$ nên $\gcd(p-1, 3) = 1$. Khi đó tồn tại phần tử $d$ là nghịch đảo của $3$ modulo $p-1$.

Suy ra phương trình $x^3 \equiv a \pmod p$ có nghiệm $a^d = x \pmod p$.

Nói cách khác mọi phần tử đều là số bậc ba modulo $p$.

---

<!-- ### Chapter 4

**Câu 4.1.** $d = 561517$, $N=661643$, $sig = 206484$

---

**Câu 4.2.** $S$ and $S''$

---

**Câu 4.3.** $p = 212081$, $q=128311$

$\Rightarrow d = 18408628619 \Rightarrow S = D^d \pmod N = 22054770669$

---

**Câu 4.4.** With $c = m^{e_B} \pmod{N_B}$ and $s = Hash(m)^{d_A} \pmod{N_A}$

$\Rightarrow c^{d_B} = m^{e_B\cdot d_B} \pmod{N_B} = m$ and $s^{e_A} = Hash(m)^{d_A \cdot e_A} \pmod{N_A} = Hash(m)$. Hence this method works


**Câu 4.5.** $A = g^a \pmod p = 2065$

$S_1 = g^k \pmod p = 3534$

$S_2 = (D-a\cdot S_1)K^{-1} \pmod{p-1} = 5888$

Hence signature is $(S_1, S_2) = (3534, 5888)$

---

**Câu 4.6.** $A^{S_1} \cdot S_1^{S_2} \equiv g^D \pmod p$

$\Rightarrow (S_1^", S_2^")$ is valid signature.

---

**Câu 4.8.** $S_1 = S_1' = g^k \pmod p$, from here Eve can know at first glance that the same random element $k$ is used
        
$S_2 = (D-aS_1)k^{-1} \pmod{p-1}$, $S_2' = (D'-aS_1')k^{-1} \pmod{p-1}$

$\Rightarrow S_2 - S_2' \equiv (D - D')k^{-1} \pmod{p-1}$ (as $aS_1 = aS_2$)

$\Rightarrow k = (D-D')(S_2-S_2')^{-1} \pmod{p-1}$

Here we get $D - aS_1 = S_2 k \pmod{p-1}$

$\Rightarrow \begin{cases}
    a = (D - S_2 k) S_1{-1} \pmod{p-1} \\ a = (D'-S_2' k) S_1^{-1} \pmod{p-1}
\end{cases}$

---

**Câu 4.9.** $p \equiv 1 \pmod q$, $1 \leqslant a \leqslant q-1$, $A=g^a \pmod p$, $S_1 = (g^k \bmod p) \bmod q$, $S_2 = (D + aS_1) k^{-1} \pmod q$

<!-- Verify: $V_1 = D \cdot S_2^{-1} \pmod q$, $V_2 = S_1 S_2^{-1} \pmod q$. We need to prove that $(g^{V_1} \cdot A^{V_2} \bmod p) \bmod q = S_1$

Here we have

$$\begin{align*}
    g^{V_1} \cdot A^{V_2} & \equiv g^{D \cdot S_2^{-1}} \cdot g^{aS_1 S_2^{-1}} \pmod p \\ & \equiv g^{(D+aS_1)S_2^{-1}} \pmod p \\ & \equiv g^k \pmod p
\end{align*}$$

$\Rightarrow (g^{V_1} A^{V_2} \bmod p) \bmod q = S_1$

---

**Câu 4.10.** $(p, q, g) = (22531, 751, 4488)$. Public key $A = 22476$ $\Rightarrow$ Not valid.

---

**Câu 4.11.** $A = g^a \pmod p$. $A = 31377$, $g = 21947$, $p = 103687 \Rightarrow a = 602$

$S_1 = (g^k \bmod p) \bmod q = 439$

$S_2 = (D + aS_1)k^{-1} \pmod q = 1259$ -->

### Chapter 7. Lattices and Cryptography

**Câu 7.43.** $t = \dfrac{\bm{b}_1 \cdot \bm{b}_2}{\lVert \bm{b}_1 \rVert^2}$ và $\bm{b}_2^* = \bm{b}_2 - t \bm{b}_1$ nên suy ra

$$\begin{equation*}
    \bm{b}_2^* \cdot \bm{b}_1 = \bm{b}_1 (\bm{b}_2 - t \bm{b}_1) = \bm{b}_1 \cdot \bm{b}_2 - t \lVert \bm{b}_1 \rVert^2 = \bm{b}_1 \cdot \bm{b}_2 - \dfrac{\bm{b}_1 \cdot \bm{b}_2}{\lVert \bm{b}_1 \rVert^2} \cdot \lVert \bm{b}_1 \rVert^2 = 0
\end{equation*}$$

Do đó $\bm{b}_2^* \perp \bm{b}_1$ và $\bm{b}_2^*$ là hình chiếu của $\bm{b}_2$ lên orthogonal complement của $\bm{b}_1$.

---

**Câu 7.44.** $\lVert \bm{a} - t \bm{b} \rVert^2 = (\bm{a} - t \bm{b})^2 = \bm{a}^2 - 2t \bm{a} \cdot \bm{b} + t^2 \bm{b}^2 = \lVert \bm{a} \rVert^2 + t^2 \lVert \bm{b} \rVert^2 - 2t \bm{a} \cdot \bm{b} \geqslant 0$ với mọi $t \in \mathbb{R}$.

Cho $\bm{a} - t \bm{b} = 0$ ta có $t = \dfrac{\bm{a} \cdot \bm{b}}{\lVert \bm{b} \rVert^2}$.

Từ đó ta có $(\bm{a} - t \bm{b}) \cdot \bm{b} = \bm{a} \cdot \bm{b} - t \lVert \bm{b} \rVert^2 = \bm{a} \cdot \bm{b} - \dfrac{\bm{a} \cdot \bm{b}}{\lVert \bm{b} \rVert^2} \cdot \lVert \bm{b} \rVert^2 = 0$.

Vì vậy $\bm{a} - t \bm{b}$ là hình chiếu của $\bm{a}$ lên orthogonal complement của $b$ (tương tự 7.43).

---

**Câu 7.45.** Thuật toán Gauss's lattice reduction.

````{prf:algorithm} Thuật toán Gauss's latice reduction
1. While True
    1. If $\lVert \bm{v}_2 \rVert < \lVert \bm{v}_1 \rVert$
        1. swap $\bm{v}_1$ and $\bm{v}_2$	
        2. $m \gets \lfloor \bm{v}_1 \cdot \bm{v}_2 / \lVert \bm{v}_1 \rVert^2 \rceil$
    2. EndIf
    3. If $m = 0$
        1. return $(\bm{v}_1, \bm{v}_2)$
    4. EndIf
    5. Replace $\bm{v}_2$ with $\bm{v}_2 - m\bm{v}_1$
2. EndWhile
````

$\bm{v}_1 = (14, -47)$, $\bm{v}_2 = (-362, -131)$, 6 steps.

$\bm{v}_1 = (14, -47)$, $\bm{v}_2 = (-362, -131)$, 6 steps.

$\bm{v}_1 = (147, 330)$, $\bm{v}_2 = (690, -207)$, 7 steps.

---

**Câu 7.46.** Do $W^\perp$ là orthogonal complement của $W$ trong $V$ nên nếu $\bm{z} \in W^\perp$ thì $\bm{z} \cdot \bm{y} = 0$, với mọi $\bm{y} \in W$.

Với hai vector $\bm{z}_1, \bm{z}_2 \in W^\perp$ ta có $\bm{z}_1 \cdot \bm{y} = \bm{z}_2 \cdot \bm{y} = 0$, với mọi $\bm{y} \in W$.

Như vậy $(\bm{z}_1 + \bm{z}_2) \cdot \bm{y} = 0 \Rightarrow \bm{z}_1 + \bm{z}_2 \in W^\perp$.

Ta lại có $\alpha \bm{z}_1 \cdot \bm{y} = \alpha \cdot 0 = 0 \Rightarrow \alpha\bm{z}_1 \in W^\perp$ với mọi $\alpha \in \mathbb{R}$.

Tới đây ta có hai cách giải.

**Cách 1.** Ta có $W \cup W^\perp = \{\bm{0}\}$. Nếu $\bm{u}$ thuộc cả hai tập $W$ và $W^\perp$ thì $\bm{u} \cdot \bm{u} = 0 \Rightarrow \bm{u} = \bm{0}$.

Ký hiệu $U = W + W^\perp$, ta chứng minh $W = V$.

Ta có thể chọn một cơ sở trực chuẩn (orthonormal basis) trong $U$ và mở rộng nó thành cơ sở trực chuẩn trong $V$. 

Khi đó, nếu $U \neq V$ thì có một phần tử $\bm{e}$ trong cơ sở của $V$ vuông góc với $U$. Do $U$ chứa $W$ và $\bm{e}$ vuông góc với $U$ nên $\bm{e} \in W^\perp$. 

Phần sau là không gian con của $W$, do đó $e$ thuộc $W$, mâu thuẫn.

**Cách 2.** Đặt $\{ \bm{e}_1, \bm{e}_2, \cdots, \bm{e}_k \}$ là cơ sở trực chuẩn của không gian con $W$. Với mỗi $\bm{v} \in V$, đặt

$$P(\bm{v}) = \sum_{j=1}^{k} (\bm{v} \cdot \bm{e}_j)  \cdot \bm{e}_j$$

Khi đó với mọi $\bm{v} \in V$ thì $\bm{v} = \underbrace{P(\bm{v})}_{\in W} + \underbrace{(\bm{v} - P(\bm{v}))}_{\in W^\perp}$.

Ở đây $\bm{v} - P(\bm{v}) \in W^\perp$ là vì nếu $j \in \{ 1, 2, \cdots, k \}$ thì 

$$\begin{align*}
    (\bm{v} - P(\bm{v})) \cdot e_j & = \left(\bm{v} - \sum_{l=1}^{k} (\bm{v} \cdot \bm{e}_l) \cdot \bm{e}_l \right) \cdot \bm{e}_j \\
        & = \bm{v} \cdot \bm{e}_j - \bm{v} \cdot \bm{e}_j = 0	
\end{align*}$$

Do $\{ \bm{e}_1, \cdots, \bm{e}_k \}$ là cơ sở của $W$, điều này cho ta $\bm{v} - P(\bm{v}) \in W^\perp$.

Như vậy

$$\begin{align*}
    \lVert \bm{v} \rVert^2 & = (a \bm{w} + b \bm{w}')^2 = a^2 \bm{w}^2 + 2ab \bm{w} \bm{w}' + b^2 \bm{w}'^2 \\
    & = a^2 \lVert \bm{w} \rVert^2 + 0 + b^2 \lVert \bm{w}' \rVert^2 = a^2 \lVert \bm{w} \rVert^2 + b^2 \lvert \bm{w}' \rVert^2.
\end{align*}$$
