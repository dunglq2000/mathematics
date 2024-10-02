## Biến đổi Fourier rời rạc

### Giới thiệu

Cho số $t \in \mathbb{N}$ và $n = 2^t$. Đặt $R$ là vành với đơn vị $1$. Vành $R$ chứa phần tử $2^{-1}$ là nghịch đảo của phần tử $2$. Biết rằng $R$ cũng chứa phần tử $\zeta_{2n}$ là một nghiệm cố định nào đó của phương trình $x^n + 1 = 0$. Đặt $\zeta_n = \zeta_{2n}^2$.

````{prf:lemma}
:label: z2n

Phần tử $\zeta_{2n}$ sinh ra một nhóm vòng (cyclic group) với order $2n$ trong nhóm nhân của vành $R$.
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Do $\zeta_{2n}$ là nghiệm của phương trình $x^n + 1 = 0$ nên $\zeta_{2n}^n = -1$, hay $\zeta_{2n}^{2^t} = -1$. Suy ra $\left(\zeta_{2n}^{2^t}\right)^2 = 1$ nên order của phần tử $\zeta_{2n}$ là $2^{t+1} = 2n$.
```

Gọi $(f_0, \ldots, f_{n-1}) \in R^n$ là vector bất kì. Khi đó:

1. **Biến đổi Fourier loại 1** của vector trên là vector $n$ chiều $(\hat f_0, \ldots, \hat f_{n-1})$ thuộc $R^n$ xác định bởi đẳng thức:

$$\hat f_i = \sum_{j=0}^{n-1} \zeta_n^{ij} f_j, \quad i = 0, 1, \ldots, n-1$$

2. **Biến đổi Fourier loại 2** là vector $n$ chiều $(\check f_1, \check f_3, \ldots, \check f_{2n-1})$ thuộc $R^n$ xác định bởi đẳng thức:

$$\check f_i = \sum_{j=0}^{n-1} \zeta_{2n}^{ij}, \quad i = 1, 3, \ldots, 2n-1$$

````{prf:remark}
Các phần tử $\hat f_i$ là giá trị của đa thức $F(x) = \sum\limits_{j=0}^{n-1} f_j x^j \in R[x]$ tại điểm $x = \zeta_n^i$, các phần tử $\check f_i$ là giá trị của đa thức $F(x)$ tại $x = \zeta_{2n}^i$ khi $i$ lẻ.
````

````{prf:lemma}
:label: fi

Ta có các đẳng thức sau:

$$f_i = n^{-1} \sum_{j=0}^{n-1} \hat f_j \zeta_n^{-ij}$$ (fi-fhat)

$$f_i = n^{-1} \sum_{\substack{1 \leqslant j \leqslant 2n-1 \\ j \ \text{lẻ}}} \check f_j \zeta_{2n}^{-ij}$$ (fi-fcheck)

với $n^{-1} = (2^{-1})^t \in R$.
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Đặt $k \in \mathbb{Z}$. Khi đó $\zeta_{2n}^{-k} = \zeta_{2n}^{2nr - k}$ với $r \in \mathbb{Z}$, $2nr - k \geqslant 0$. Ngoài ra, vì order của phần tử $\zeta_n$ trong phép nhân là $n$ nên ta có phương trình hệ quả

$$\sum_{j = 0}^{n - 1} \zeta_n^{lj} = n \quad \text{khi} \quad l \equiv 0 \pmod n$$ (l0)

$$\sum_{j = 0}^{n - 1} \zeta_n^{lj} = 0 \quad \text{khi} \quad l \not\equiv 0 \pmod n$$ (l1)

Phương trình {eq}`fi-fhat` thỏa mãn vì:

$$\sum_{j=0}^{n-1} \hat f_j \zeta_n^{-ij} = \sum_{j=0}^{n-1} \sum_{k=0}^{n-1} f_k \zeta_n^{jk} \zeta_n^{-ij} = \sum_{k=0}^{n-1} f_k \sum_{j=0}^{n-1} \zeta_n^{(k-i)j} = n f_i$$

theo {eq}`l0` và {eq}`l1`.

Đẳng thức {eq}`fi-fcheck` có được từ

$$\begin{align*}
    \sum_{\substack{j \leqslant j \leqslant 2n - 1 \\ j \ \text{lẻ}}} \check f_j \zeta_{2n}^{-ij} & = \sum_{k=0}^{n-1} \check f_{2k+1} \zeta_{2n}^{-i(2k+1)} \\ 
    & = \sum_{k=0}^{n-1} \sum_{l=0}^{n-1} f_l \zeta_{2n}^{l(2k+1)} \zeta_{2n}^{-i(2k+1)} \\
    & = \sum_{l=0}^{n-1} f_l \zeta_{2n}^{l-i} \sum_{k=0}^{n-1} \zeta_n^{(l-i) k}.
\end{align*}$$

Từ {eq}`l0` và {eq}`l1` suy ra được đẳng thức {eq}`fi-fcheck`.
```

Việc tính toán biến đổi Fourier rời rạc bằng {eq}`fi-fhat` và {eq}`fi-fcheck` cần $O(n^2)$ phép tính cộng và nhân trong vành $R$. Phần sau sẽ trình bày phương pháp tính biến đổi Fourier rời rạc với độ phức tạp $O(n \log n)$. Phương pháp đó được gọi là **biến đổi Fourier nhanh** (hay **Fast Fourier Transform**, **FFT**, **быстрое преобразование Фурье**).

### Tính toán biến đổi Fourier

````{prf:theorem}
:label: fhat-fcheck
Biến đổi Fourier rời rạc $(\hat f_0, \ldots, \hat f_{n-1})$ có thể được tính bằng $nt$ phép cộng trên vành $R$ và $nt$ phép nhân cho lũy thừa của $\zeta_n$ trên vành $R$.

Biến đổi Fourier rời rạc $(\check f_1, \ldots, \check f_{2n-1})$ có thể được tính bằng $nt$ phép cộng trên vành $R$ và $nt$ phép nhân cho lũy thừa của $\zeta_{2n}$ trên vành $R$.

Nếu có $(\hat f_i)$ và $(\check f_i)$ thì có thể tính được vector $(f_0, \ldots, f_{n-1})$ bằng $nt$ phép cộng trên vành $R$, $nt$ phép nhân cho lũy thừa của $\zeta_{2n}$ trên vành $R$ và $n$ phép nhân cho $n^{-1} \in R$.
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Đặt

$$\begin{align*}
    F(x) = \sum_{j=0}^{n-1} f_i x^i & = \sum_{\substack{0 \leqslant j \leqslant n-1 \\ j \ \text{chẵn}}} f_j x^j + \sum_{\substack{0 \leqslant j \leqslant n-1 \\ j \ \text{lẻ}}} f_j x^j \\
    & = F_0(x^2) + x F_1(x^2),
\end{align*}$$

với $\deg F_0(x)$ và $\deg F_1(x) < \dfrac{n}{2} = 2^{t-1}$. Khi đó

$$
    F(\zeta_n^i) = F_0(\zeta_n^{2i}) + \zeta_n^i F_1(\zeta_n^{2i}),
$$ (F)

với $i = 0, \ldots, n-1$.

Kí hiệu $\zeta_{n/2} = \zeta_n^2$. Khi đó

$$\{ \zeta_n^{2i} \mid 0 \leqslant i \leqslant n - 1 \} = \{ \zeta_{n/2}^i \mid 0 \leqslant i \leqslant \dfrac{n}{2} - 1\}$$

Dựa trên quy nạp ta tính được biến đổi Fourier rời rạc loại 1, tức là tính $(F(\zeta_n^0), \ldots, F(\zeta_n^{n-1}))$ theo công thức {eq}`F` bằng $n$ phép tính cộng trong $R$ và $n$ phép tính nhân cho lũy thừa của $\zeta_n$ trong $R$, nếu ta đã biết các giá trị $F_0(\zeta_{n/2}^i)$ và $F_1(\zeta_{n/2}^i)$ với $i = 0, \ldots, \dfrac{n}{2} - 1$.

Nếu $t = 1$ và $n = 2 =2^t$ (bước cơ sở quy nạp) thì để tính $(\hat f_0, \hat f_1)$ ta cần tìm $F_0 + \zeta_2^i F_1$, với $F_0$ và $F_1$ là các phần tử vành $R$, $i = 0, 1$.

Như vậy, với $n=2$ thì cần $2 = nt$ phép nhân cho lũy thừa của $\zeta_n = \zeta_2$ trong $R$ và $2 = nt$ phép cộng trong $R$.

Giả sử với mọi $j < t$, để tính biến đổi Fourier rời rạc loại 1 trên vector $2^j$ chiều ta cần $2^j \cdot j$ phép nhân cho lũy thừa của $\zeta_{2^j} = \left(\zeta_n\right)^{2^{t-j}}$ trong $R$, và $2^j \cdot j$ phép cộng trong $R$.

Khi đó, nếu $j = t$ thì việc tính $(\hat f_0, \ldots, \hat f_{n-1})$ theo công thức {eq}`F` bao gồm tính $F_0(\zeta_{n/2}^i)$ và $F_1(\zeta_{n/2}^i)$ với $i = 0, \ldots, n-1$. Nói cách khác là tính biến đổi Fourier cho vector độ dài $n / 2$ gồm các hệ số $F_0(x)$ và $F_1(x)$ cộng thêm $n$ phép cộng trong $R$ và $n$ phép nhân cho lũy thừa của $\zeta_n$ trong $R$.

Khi đó, theo bước quy nạp, việc tính vector $(\hat f_0, \ldots, \hat f_{n-1})$ cần không quá $n$ phép cộng trong $R$, cộng với $n$ phép nhân trong $R$, cộng với $2 \cdot 2^{t-1} \cdot (t-1)$ phép nhân cho lũy thừa của $\zeta_n$ trong $R$. Như vậy cần tổng cộng $n + n(t - 1) = nt$ phép cộng trong $R$ và $n + n(t-1) = nt$ phép nhân cho lũy thừa của $\zeta_n$ trong $R$. Như vậy mệnh đề đầu tiên của định lý được chứng minh.

Mệnh đề thứ hai chứng minh tương tự, ta thay $\zeta_n$ thành $\zeta_{2n}$.

Mệnh đề thứ ba suy ra từ hai mệnh đề trên và {prf:ref}`fi`.
```

### Biến đổi Fourier và phép nhân đa thức

````{prf:lemma}
Một phép nhân trong vành $R[x]/(x^{2^t} + 1)$ có thể tính bởi $n=2^t$ phép nhân trong $R$, $3nt$ phép cộng trong $R$, $3nt$ phép nhân cho lũy thừa của $\zeta_{2n}$ trong $R$ và $n$ phép nhân cho $n^{-1}$ trong $R$.
````

````{prf:remark}
Bổ đề không áp dụng khi $R = \mathbb{Z}$ và $R = \mathbb{Q}$ vì hai vành này không có phần tử $\zeta_{2n}$ ($n$-root của đơn vị).
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Đặt $\sum\limits_{i=0}^{n-1} f_i x^i$ và $\sum\limits_{i=0}^{n-1} g_i x^i$, $F, G \in R[x]$ và là các lớp nhân tử nào đó của $R[x] / (x^{2^t} + 1)$.

Đặt $H = \sum\limits_{i=0}^{n-1} h_i x^i \in R[x]$ sao cho $FG \equiv H \pmod{x^n+1}$. Nói cách khác $H$ là tích $F \cdot G$ trong vành.

Biến đổi Fourier loại 2 cho vector $(f_0, \ldots, f_{n-1})$ và $(g_0, \ldots, g_{n-1})$ cho ta phương trình

$$\check f_i \check g_i = F(\zeta_{2n}^i) G(\zeta_{2n}^i = H(\zeta_{2n}^i) = \check h_i)$$

với $i$ lẻ, $1 \leqslant i \leqslant 2n-1$, vì $\zeta_{2n}^n + 1 = 0$.

Như vậy nếu ta biết tất cả $\check f_i$ và $\check g_i$ thì có thể tính mọi $\check h_i$ với $n$ phép nhân trong $R$.

Theo {prf:ref}`fhat-fcheck` các phần tử $\check f_i$ và $\check g_i$ có thể tính với $2tn$ phép cộng trong $R$ và $2tn$ phép nhân cho lũy thừa của $\zeta_{2n}$ trong $R$. Từ đó các phần tử $h_i$ có thể tính, với điều kiện đã biết $\check h_i$, với $tn$ phép cộng trong $R$, $tn$ phép nhân cho lũy thừa của $\zeta_{2n}$ trong $R$ và $n$ phép nhân cho phần tử $n^{-1}$ trong $R$. Ta có điều phải chứng minh.
```

````{prf:corollary}
Đặt $T$ là vành giao hoán với đơn vị, $2^{-1} \in T$, $\zeta_{4n} = \zeta_{2^{t + 2}} \in T$ là nghiệm phương trình $x^{2n} + 1 = 0$. Nếu $F(x), G(x) \in T[x]$, $\deg F(x) < n$, $\deg G(x) < n$ thì tích $F(x) \cdot G(x)$ có thể tính với $2n$ phép nhân trong $T$, $6n(t+1)$ phép cộng trong $T$, $6n(t+1)$ phép nhân cho lũy thừa của $\zeta_{4n}$ trong $T$ và $2n$ phép nhân cho $(2^{-1})^{t+1}$.
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Do các chặn của bậc đa thức $F(x)$ và $G(x)$ nên bậc của $F(x) \cdot G(x)$ sẽ nhỏ hơn $2n$, do đó giống với phần dư khi chia $F(x) \cdot G(x)$ cho $2^{2n} + 1$. Khi đó tích $F(x) \cdot G(x)$ trong $R[x]$ có thể tính với một phép nhân trong $R[x] / (x^{2n} + 1)$. Mệnh đề này suy ra từ {prf:ref}`z2n`, ta thay $n$ thành $2n$ và $t$ thay thành $t+1$.
```
