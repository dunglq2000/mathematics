## Biến đổi Fourier rời rạc

### Giới thiệu

Cho số $t \in \mathbb{N}$ và $n = 2^t$. Đặt $R$ là vành với đơn vị $1$. Vành $R$ chứa phần tử $2^{-1}$ là nghịch đảo của phần tử $2$. Biết rằng $R$ cũng chứa phần tử $\zeta_{2n}$ là một nghiệm cố định nào đó của phương trình $x^n + 1 = 0$. Đặt $\zeta_n = \zeta_{2n}^2$.

````{prf:lemma}
Phần tử $\zeta_{2n}$ sinh ra một nhóm vòng (cyclic group) từ nhóm nhân của vành $R$.
````

Gọi $(f_0, \ldots, f_{n-1}) \in R^n$ là vector bất kì. Khi đó:

1. **Biến đổi Fourier loại 1** của vector trên là vector $n$ chiều $(\hat f_0, \ldots, \hat f_{n-1})$ thuộc $R^n$ xác định bởi đẳng thức:

$$\hat f_i = \sum_{j=0}^{n-1} \zeta_n^{ij} f_j, \quad i = 0, 1, \ldots, n-1$$

2. **Biến đổi Fourier loại 2** là vector $n$ chiều $(\check f_1, \check f_3, \ldots, \check f_{2n-1})$ thuộc $R^n$ xác định bởi đẳng thức:

$$\check f_i = \sum_{j=0}^{n-1} \zeta_{2n}^{ij}, \quad i = 1, 3, \ldots, 2n-1$$

````{prf:remark}
Các phần tử $\hat f_i$ là giá trị của đa thức $F(x) = \sum\limits_{j=0}^{n-1} f_j x^j \in R[x]$ tại điểm $x = \zeta_n^i$, các phần tử $\check f_i$ là giá trị của đa thức $F(x)$ tại $x = \zeta_{2n}^i$ khi $i$ lẻ.
````

````{prf:lemma}
Ta có các đẳng thức sau:

$$f_i = n^{-1} \sum_{j=0}^{n-1} \hat f_j \zeta_n^{-ij}$$

$$f_i = n^{-1} \sum_{\substack{1 \leqslant j \leqslant 2n-1 \\ j \ \text{lẻ}}} \check f_j \zeta_{2n}^{-ij}$$

với $n^{-1} = (2^{-1})^t \in R$.
````

### Tính toán biến đổi Fourier

````{prf:theorem}
Biến đổi Fourier rời rạc $(\hat f_0, \ldots, \hat f_{n-1})$ có thể được tính bằng $nt$ phép cộng trên vành $R$ và $nt$ phép nhân trên vành $R$ theo lũy thừa của phần tử $\zeta_n$.

Biến đổi Fourier rời rạc $(\check f_1, \ldots, \check f_{2n-1})$ có thể được tính bằng $nt$ phép cộng trên vành $R$ và $nt$ phép nhân trên vành $R$ theo lũy thừa của phần tử $\zeta_{2n}$.

Nếu có $(\hat f_i)$ và $(\check f_i)$ thì có thể tính được vector $(f_0, \ldots, f_{n-1})$ bằng $nt$ phép cộng trên vành $R$, $nt$ phép nhân trên vành $R$ theo lũy thừa của $\zeta_{2n}$ và $n$ phép nhân cho $n^{-1} \in R$.
````

### Biến đổi Fourier và phép nhân đa thức

````{prf:lemma}
Một phép nhân trong vành $R[x]/(x^{2^t} + 1)$ có thể tính bởi $n=2^t$ phép nhân trong $R$, $3nt$ phép cộng trong $R$, $3nt$ phép nhân trong $R$ cho lũy thừa $\zeta_{2n}$ và $n$ phép nhân trong $R$ cho $n^{-1}$.
````

````{prf:remark}
Bổ đề không áp dụng khi $R = \mathbb{Z}$ và $R = \mathbb{Q}$ vì hai vành này không có phần tử $\zeta_{2n}$ ($n$-root của đơn vị).
````

````{prf:corollary}
Đặt $T$ là vành giao hoán với đơn vị, $2^{-1} \in T$, $\zeta_{4n} = \zeta_{2^{t + 2}} \in T$ là nghiệm phương trình $x^{2n} + 1 = 0$. Nếu $F(x), G(x) \in T[x]$, $\deg F(x) < n$, $\deg G(x) < n$ thì tích $F(x) \cdot G(x)$ có thể tính với $2n$ phép nhân trong $T$, $6n(t+1)$ phép cộng trong $T$, $6n(t+1)$ phép nhân trong $T$ theo lũy thừa của $\zeta_{4n}$ và $2n$ phép nhân cho $(2^{-1})^{t+1}$.
````