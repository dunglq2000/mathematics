# Abstract Algebra: Theory and Applications

Lời giải cho quyển sách **Abstract Algebra: Theory and Applications** của Thomas W. Judson {cite}`Judson2012`.

## Chương 3. Groups

```{admonition} Bài 7
Đặt $S = \mathbb{R} \setminus \{-1\}$ và định nghĩa toán tử 2 ngôi trên $S$ là $a \star b = a + b + ab$. Chứng minh rằng $(S, \star)$ là nhóm Abel.
```

Để chứng minh $(S, \star)$ là nhóm ta chứng minh 3 tiên đề của nhóm.

1. Giả sử tồn tại phần tử đơn vị $e$, khi đó $e \star s = s \star e = s$ với mọi $s \in S$. Nghĩa là $e + s + es = s + e + se = s$. Vậy $e + se = 0$ mà $s \neq -1$ nên $e = 0$
2. Với $e = 0$, giả sử với mọi $s \in S$ có nghịch đảo $s'$. Do $s \star s' = s' \star s = e$ nên $s + s' + ss' = s' + s + s's = e = 0$, tức là $s'(1 + s) = -s$. Vậy $s' = \dfrac{-s}{1 + s}$
3. Với mọi $a, b, c \in S$, 

$$\begin{align*}
    a \star (b \star c) & = a \star (b + c + bc) = a + (b+c+bc) + a (b+c+bc) \\ 
    & = a + b + c + ab + bc + ca + abc
\end{align*}$$

và

$$\begin{align*}
    (a \star b) \star c & = (a + b + ab) \star c = a + b + ab + c + c(a+b+bc) \\
    & = a + b + c + ab + bc + ca + abc.
\end{align*}$$

Như vậy $a \star (b \star c) = (a \star b) \star c$, do đó $\star$ có tính kết hợp.

Vậy $(S, \star)$ là nhóm.

```{admonition} Bài 39
Gọi $G$ là tập các ma trận $2 \times 2$ với dạng

$$\begin{pmatrix}
    \cos \theta & -\sin \theta \\ \sin \theta & \cos \theta
\end{pmatrix}$$

với $\theta \in \mathbb{R}$. Chứng minh rằng $G$ là subgroup của $SL_2 (\mathbb{R})$.
```

Với $\theta_1, \theta_2 \in \mathbb{R}$, ta có

$$\begin{align*}
& \begin{pmatrix}
    \cos \theta_1 & -\sin \theta_1 \\ \sin \theta_1 & \cos \theta_1
\end{pmatrix} \begin{pmatrix}
    \cos \theta_2 & -\sin \theta_2 \\ \sin \theta_2 & \cos \theta_2
\end{pmatrix} \\
= & \begin{pmatrix}
    \cos \theta_1 \cos \theta_2 - \sin \theta_1 \sin \theta_2 & -\cos \theta_1 \sin \theta_2 - \sin \theta_1 \cos \theta_2 \\ 
    \sin \theta_1 \cos \theta_2 + \cos \theta_1 \sin \theta_2 & -\sin \theta_1 \sin \theta_2 + \cos \theta_1 \cos \theta_2
\end{pmatrix} \\
= & \begin{pmatrix}
    \cos (\theta_1 + \theta_2) & -\sin (\theta_1 + \theta_2) \\
    \sin (\theta_1 + \theta_2) & \cos (\theta_1 + \theta_2)
\end{pmatrix}
\end{align*}$$

Suy ra định thức của tích 2 ma trận là

$$\begin{align*}
    \det \Biggl(\begin{pmatrix}
        \cos (\theta_1 + \theta_2) & -\sin (\theta_1 + \theta_2) \\
        \sin (\theta_1 + \theta_2) & \cos (\theta_1 + \theta_2)
    \end{pmatrix}\Biggr)
    = & 1 \cdot 1 = 1
\end{align*}$$

Như vậy phép nhân 2 ma trận có dạng trên đóng trên $SL_2 (\mathbb{R})$.

Phần tử đơn vị là $\begin{pmatrix}
1 & 0 \\ 0 & 1
\end{pmatrix}$ tương ứng với $\theta = 0$.

Phần tử nghịch đảo là $\begin{pmatrix}
\cos (-\theta) & -\sin (-\theta) \\ \sin (-\theta) & \cos (-\theta)
\end{pmatrix}$ suy ra từ công thức định thức ban nãy.

Cuối cùng, phép nhân ma trận có tính kết hợp. Như vậy $G$ là subgroup của $SL_2 (\mathbb{R})$.      

```{admonition} Bài 47
Đặt $G$ là nhóm và $g \in G$. Chứng minh rằng

$$Z(G) = \{ x \in G: gx = xg \; \forall \; g \in G \}$$

là subgroup của $G$. Subgroup này gọi là **center** của $G$.
```

Giả sử trong $G$ có 2 phần tử là $x_1$ và $x_2$ thuộc $Z(G)$. Khi đó

$$x_1 g = g x_1 \text{ và } x_2 g = g x_2 \text{ với mọi } g \in G.$$

Xét phần tử $x_1 x_2$, ta có

$$(x_1 x_2) g = x_1 (x_2 g) = x_1 (g x_2) = (g x_1) x_2 = g (x_1 x_2)$$

với mọi $g \in G$. Do đó $x_1 x_2 \in Z(G)$ nên $Z(G)$ là subgroup.

```{admonition} Bài 49
Cho ví dụ về nhóm vô hạn mà mọi nhóm con không tầm thường của nó đều vô hạn.
```

Ví dụ tập $\mathbb{Z}$ và phép cộng số nguyên. Khi đó mọi nhóm con của $\mathbb{Z}$ có dạng $n\mathbb{Z}$ với $n \in \mathbb{Z}$. Ví dụ

$2\mathbb{Z} = \{\cdots, -4, -2, 0, 2, 4, \cdots\}$ với phần tử sinh là $2$

$n\mathbb{Z} = \{\cdots, -2n, -n, 0, n, 2n, \cdots\}$ với phần tử sinh là $n$

```{admonition} Bài 54
Cho $H$ là subgroup của $G$ và

$$C(H) = \{g \in G: gh = hg \; \forall \; h \in H\}.$$

Chứng minh rằng $C(H)$ là subgroup của $G$. Subgroup này được gọi là **centralizer** của $H$ trong $G$.
```

Gọi $g_1$ và $g_2$ thuộc $C(H)$. Khi đó $g_1 h = h g_1$ và $g_2 h = h g_2$ với mọi $h \in H$

Xét phần tử $g_1 g_2$, với mọi $h \in H$ ta có

$$(g_1 g_2) h = g_1 (g_2 h) = g_1 (h g_2) = (g_1 h) g_2 = (h g_1) g_2 = h (g_1 g_2).$$

Như vậy $g_1 g_2 \in C(H)$, từ đó $C(H)$ là subgroup của $G$

## Chương 5. Permutation Groups

```{admonition} Bài 13
Đặt $\sigma = \sigma_1 \cdots \sigma_m \in S_n$ là tích của các cycle độc lập. Chứng minh rằng order của $\sigma$ là LCM của độ dài các cycle $\sigma_1, \cdots, \sigma_m$.
```

Đặt $l_i$ là độ dài cycle $\sigma_i$ ($i = 1, \cdots m$). Khi đó $\sigma_i^{k_i l_i}$ sẽ ở dạng các cycle độ dài 1 ($k_i \in \mathbb{Z}$).

Từ đó, $\sigma^l = \sigma_1^l \cdots \sigma_m^l = (1)\cdots(n)$ nếu $l = k_1 l_1 = \cdots k_m l_m$. Số $l$ nhỏ nhất thỏa mãn điều kiện này là $\text{lcm} (l_1, \cdots, l_m)$ (đpcm).

```{admonition} Bài 23
Nếu $\sigma$ là chu trình với độ dài lẻ, chứng minh rằng $\sigma^2$ cũng là chu trình.
```

Giả sử $\sigma = (g_1, g_2, \cdots, g_{n-1}, g_n)$ với $n$ lẻ.

Khi đó

$$\sigma^2 = (g_1, g_3, \cdots, g_n, g_2, g_4, \cdots, g_{n-1})$$

cũng là chu trình.

```{admonition} Bài 30
Cho $\tau = (a_1, a_2, \cdots, a_k)$ là chu trình độ dài $k$.

1. Chứng minh rằng với mọi hoán vị $\sigma$ thì

$$\sigma \tau \sigma^{-1} = (\sigma(a_1), \sigma(a_2), \cdots, \sigma(a_k))$$

là chu trình độ dài $k$.

2. Gọi $\mu$ là chu trình độ dài $k$. Chứng minh rằng tồn tại hoán vị $\sigma$ sao cho $\sigma \tau \sigma^{-1} = \mu$
```

Để chứng minh hai mệnh đề trên ta cần chú ý một số điều.

1. Ta thấy rằng bất kì phần tử nào khác $a_1, a_2, \cdots, a_k$ thì khi qua $\tau$ không đổi, do đó khi đi qua $\sigma \tau \sigma^{-1}$ thì chỉ đi qua $\sigma \sigma^{-1}$ và cũng không đổi. Nói cách khác các phần tử $a_1, a_2, \cdots, a_k$ vẫn nằm trong chu trình nên ta có đpcm.
2. Từ câu (a), với $\mu = (b_1, b_2, \cdots, b_k)$ thì ta chọn $\sigma$ sao cho $b_i = \sigma(a_i)$.

## Chương 6. Cosets

```{admonition} Bài 11
Gọi $H$ là subgroup của nhóm $G$ và giả sử $g_1, g_2 \in G$. Chứng minh các mệnh đề sau là tương đương:

1. $g_1 H = g_2 H$
2. $H g_1^{-1} = H g_2^{-1}$
3. $g_1 H \subseteq g_2 H$
4. $g_2 \in g_1 H$
5. $g_1^{-1} g_2 \in H$ 
```

Từ (1) ra (2): Ta đã biết các coset là rời nhau hoặc trùng nhau, do đó với mọi $g_1 h \in g_1 H$, tồn tại $g_2 h' \in g_2 H$ mà $g_1 h = g_2 h'$. Suy ra $(g_1 h)^{-1} = (g_2 h')^{-1}$ hay $h^{-1} g_1^{-1} = h'^{_1} g_2^{-1}$ (đpcm).

Từ (1) ra (3): Hiển nhiên.

Từ (1) ra (4): Với mọi $g_1 h \in g_1 H$, tồn tại $g_2 h' \in g_2 H$ sao cho $g_1 h = g_2 h'$, hay $g_2 = g_1 h h'^{-1}$, đặt $h'' = h h'^{-1}$ thì $h'' \in H$ ($H$ là nhóm con) nên $g_1 h'' \in g_1 H$. Suy ra $g_2 \in g_1 H$.

Từ (1) ra (5): Tương tự, ta có $g_1 h = g_2 h'$, suy ra $h h'^{-1}= g_1^{-1} g_2 \in H$.

```{admonition} Bài 16
Nếu $g h g^{-1} \in H$ với mọi $g \in G$ và $h \in H$, chứng minh rằng right coset trùng với left coset.
```

Do $g h g^{-1} \in H$ nên tồn tại $h' \in H$ sao cho $g h g^{-1} = h'$. Tương đương $g h = h' g$ với mọi $h \in H$ nên $g H = H g$. Điều này đúng với mọi $g \in G$ nên các right coset trùng left coset.

```{admonition} Bài 17
Giả sử $[G:H]=2$. Chứng minh rằng nếu $a, b$ không thuộc $H$ thì $ab \in H$.
```

Ta biết rằng 2 coset ứng với 2 phần tử $g_1, g_2$ bất kì là trùng nhau hoặc rời nhau.

Do đó với $eH = H$, ta suy ra 2 coset của $G$ là $H$ và $G \setminus H$.

Vì $a, b \not\in H$ nên coset của chúng trùng nhau. Và nghịch đảo của $a$ cũng nằm trong $G \setminus H$ vì nếu nghịch đảo của $a$ nằm trong $H$ thì $a$ cũng phải nằm trong $H$.

Suy ra $a^{-1} H = b H$. Nghĩa là tồn tại 2 phần tử $h_1, h_2 \in H$ sao cho $a^{-1} h_1 = b h_2$, tương đương $h_1 h_2^{-1} = a b \in H$ (đpcm).

```{admonition} Bài 21
Gọi $G$ là cyclic group với order $n$. Chứng minh rằng có đúng $\phi(n)$ phần tử sinh của $G$.
```

Gọi $g$ là một phần tử sinh của $G$. Khi đó $g$ sinh ra tất cả phần tử trong $G$, hay nói cách khác các phần tử trong $G$ có dạng $g^i$ với $0 \leq i < n$.

Như vậy một phần tử $h = g^i$ cũng là phần tử sinh của $G$ khi và chỉ khi $\gcd(i, n) = 1$ và có $\phi(n)$ số $i$ như vậy (đpcm).

## Chương 9. Isomorphism

```{admonition} Bài 18
Chứng minh rằng subgroup của $\mathbb{Q}^*$ gồm các phần tử có dạng $2^m 3^n$ với $m, n \in \mathbb{Z}$ là internal direct product tới $\mathbb{Z} \times \mathbb{Z}$
```

Xét ánh xạ $\varphi: \mathbb{Q}^* \rightarrow \mathbb{Z~} \times \mathbb{Z}$, $\varphi(2^m 3^n) = (m, n)$.

Hàm này là well-defined vì với $m$ cố định thì mỗi phần tử $2^m 3^n$ chỉ cho ra một phần tử $(m, n)$. Tương tự với cố định $n$.

Hàm này là đơn ánh (one-to-one) vì với $m_1 = m_2$ và $n_1 = n_2$ thì $2^{m_1} 3^{n_1} = 2^{m_2} 3^{n_2}$.

Hàm này cũng là toàn ánh vì với mỗi cặp $(m, n)$ ta đều tính được $2^m 3^n$.

Vậy hàm $\varphi$ là song ánh.

Thêm nữa,

$$\begin{align*}
    \varphi(2^{m_1} 3^{n_1} \cdot 2^{m_2} 3^{n_2})& = \varphi(2^{m_1 + m_2} 3^{n_1 + n_2}) \\
    & = (m_1 + m_2, n_1 + n_2) = (m_1, n_1) + (m_2, n_2) \\
    & = \varphi(2^{m_1} 3^{n_1}) \varphi(2^{m_2} 3^{n_2})
\end{align*}$$

Vậy $\varphi$ là homomorphism, và là song ánh nên là isomorphism.


```{admonition} Bài 20
Chứng minh hoặc bác bỏ: mọi nhóm Abel có order chia hết bởi 3 chứa một subgroup có order là 3.
```

Gọi order của nhóm Abel là $n=3k$, và $g$ là phần tử sinh của nhóm Abel đó. Như vậy $g^n = g^{3k} = e$.

Nếu ta chọn $h = g^k$ thì $h^3 = e$, khi đó subgroup được sinh bởi $h$ có order 3 (đpcm).

```{admonition} Bài 21
Chứng minh hoặc bác bỏ: mọi nhóm không phải Abel có order chia hết bởi 6 chứa một subgroup có order 6
```

Với $\mathcal{S}_3$ có order là 6 nhưng không có nhóm con nào order 6 (nhóm con chỉ có order 1, 2 hoặc 3) (bác bỏ).

```{admonition} Bài 22
Gọi $G$ là group với order 20. Nếu $G$ có các subgroup $H$ và $K$ với order 4 và 5 mà $hk=kh$ với mọi $h \in H$ và $k \in K$, chứng minh rằng $G$ là internal direct product của $H$ và $K$.
```

Ta chứng minh $H \cap K = \{ e \}$. Giả sử tồn tại phần tử $m \in H \cap K$, khi đó do $m \in H$ nên $mk = km$ với mọi $k \in K$. Tuy nhiên $m \in K$ do đó điều này xảy ra khi và chỉ khi $m = e$.

Như vậy $H \cap K = \{ e \}$.

## Chương 11. Homomorphism

```{admonition} Bài 1
Chứng minh rằng $\det(AB) = \det(A) \det(B)$ với $A, B \in GL_2(\mathbb{R})$. Điều này chứng tỏ rằng định thức là homomorphism từ $GL_2(\mathbb{R})$ tới $\mathbb{R}^*$.
```

Đặt $A = \begin{pmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{pmatrix}$ và $B = \begin{pmatrix} b_{11} & b_{12} \\ b_{21} & b_{22} \end{pmatrix}$. Khi đó

$$\begin{equation*}
    A B = \begin{pmatrix}
        a_{11} b_{11} + a_{12} b_{21} & a_{11} b_{12} + a_{12} b_{22} \\
        a_{21} b_{11} + a_{22} b_{21} & a_{21} b_{12} + a_{22} b_{22}
    \end{pmatrix}
\end{equation*}$$
    
Như vậy ta có 

$$\begin{align*}
    \det (AB) = & (a_{11} b_{11} + a_{12} b_{21}) (a_{21} b_{12} + a_{22} b_{22}) \\
            - & (a_{11} b_{12} + a_{12} b_{22}) (a_{21} b_{11} + a_{22} b_{21}) \\ 
            = & \cancel{a_{11} a_{21} b_{11} b_{12}} + a_{11} a_{22} b_{11} b_{22} + a_{12} a_{21} b_{12} b_{21} + \bcancel{a_{12} a_{22} b_{21} b_{22}} \\ 
            - & \cancel{a_{11} a_{21} b_{11} b_{12}} - a_{11} a_{22} b_{12} b_{21} - a_{12} a_{21} b_{11} b_{22} - \bcancel{a_{12} a_{22} b_{21} b_{22}}
\end{align*}$$

Tương tự,

$$\begin{align*}
    \det (A) \det (B) = & (a_{11} a_{22} - a_{12} a_{21}) (b_{11} b_{22} - b_{12} b_{21}) \\ = & a_{11} a_{22} b_{11} b_{22} - a_{11} a_{22} b_{12} b_{21} \\ - & a_{12} a_{21} b_{11} b_{22} + a_{12} a_{21} b_{12} b_{21}
\end{align*}$$

Như vậy $\det (AB) = \det (A) \det (B)$ và do đó ánh xạ $\det$ từ $GL_2(\mathbb{R})$ tới $\mathbb{R}^*$ là homomorphism.

```{admonition} Bài 4
Xét $\phi : \mathbb{Z} \to \mathbb{Z}$ cho bởi $\phi(n) = 7n$. Chứng minh rằng $\phi$ là homomorphism. Tìm hạt nhân và ảnh của $\phi$.
```

Ta có $\phi(a+b) = 7(a+b) = 7a + 7b = \phi(a) + \phi(b)$ với mọi $a, b \in \mathbb{Z}$. Do đó $\phi$ là homomorphism. 
    
Hạt nhân của $\phi$ là tập hợp các số $n$ để $\phi(n) = 0$, hay $7 n = 0$. Như vậy $n=0$ nên $\ker \phi = \{ 0 \}$.

Ảnh của $\phi$ là tập $\{ \ldots, -2 \cdot 7, -7, 0, 7, 2 \cdot 7, \ldots \}$.

```{admonition} Bài 8
Nếu $G$ là nhóm Abel và $n \in \mathbb{N}$, chứng minh rằng $\phi : G \to G$ xác định bởi $g \mapsto g^n$ là homomorphism.
```

Với mọi $g, h \in G$ thì $\phi(gh) = (gh)^n$. Do $G$ là nhóm Abel nên ta có $(gh)^n = g^n h^n = \phi(g) \phi(h)$. Như vậy $\phi$ là đồng cấu nhóm.

```{admonition} Bài 9
Nếu $\phi : G \to H$ là homomorphism và $G$ là nhóm Abel, chứng minh rằng $\phi(G)$ cũng là nhóm Abel.
```

Với mọi $g, h \in G$, do $\phi$ là homomorphism nên $\phi(gh) = \phi(g) \phi(h)$. Do $G$ là nhóm Abel nên $gh = hg$ với mọi $g, h \in G$, suy ra $\phi(gh) = \phi(hg)$. Tương đương với $\phi(g) \phi(h) = \phi(h) \phi(g)$ nên $\phi(G)$ cũng là nhóm Abel.

```{admonition} Bài 10
Nếu $\phi : G \to H$ là homomorphism và $G$ là nhóm cyclic, chứng minh rằng $\phi(G)$ cũng là nhóm cyclic.
```

Tương tự câu 9.

```{admonition} Bài 20
Cho homomorphism $\phi : G \to H$ và định nghĩa quan hệ $\sim$ trên $G$ theo quy tắc $a, b \in G$ có quan hệ với nhau nếu $\phi(a) = \phi(b)$ và ký hiệu là $a \sim b$. Chứng minh đây là quan hệ tương đương và mô tả cách xây dựng các lớp tương đương.
```

Do $\phi$ là ánh xạ nên $\phi(a) = \phi(a)$ với mọi $a \in G$, suy ra $\sim$ có tính phản xạ.

Nếu $a \sim b$ thì $\phi(a) = \phi(b)$. Tương đương với $\phi(b) = \phi(a)$ nên $b \sim a$. Như vậy quan hệ trên có tính đối xứng.

Nếu $a \sim b$ thì $\phi(a) = \phi(b)$, và nếu $b \sim c$ thì $\phi(b) = \phi(c)$. Suy ra $\phi(a) = \phi(b) = \phi(c)$ nên $a \sim c$. Như vậy quan hệ có tính bắc cầu.

Kết luận: quan hệ $\sim$ xác định như trên là quan hệ tương đương.

Để xây dựng các lớp tương đương, đặt $I = \{ i_1, i_2, \ldots, i_m \}$ là ảnh của homomorphism $\phi$. Rõ ràng $I \subset H$. Khi đó các lớp tương đương ứng với các phần tử $i_1, i_2, \ldots, i_m$, hay

$$\begin{equation*}
    \bar{i}_j = \{ g \in G : \phi(g) = i_j \}, \quad 1 \leqslant i \leqslant m
\end{equation*}$$
