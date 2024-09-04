## Vành và trường

```{contents}
```

### Vành

````{prf:definition} Ring, Vành
Cho tập hợp $R$, trên đó ta định nghĩa hai toán tử **cộng** và **nhân**.

Khi đó, $(R, +, \times)$ tạo thành **vành** (hay **ring**) nếu

1. $(R, +)$ là nhóm Abel.
2. $(R, \times)$ có tính kết hợp với phép nhân. Với mọi $a, b, c \in R$ thì $a \times (b \times c) = (a \times b) \times c$.
3. Tính phân phối của phép cộng và phép nhân. Với mọi $a, b, c \in R$ thì $(a + b) \times c = a \times c + b \times c$.
````

Tóm lại, $(R, +, \times)$ là vành nếu nó là nhóm Abel đối với phép cộng và có tính kết hợp với phép nhân.

````{prf:remark}
Phép nhân ở đây không nhất thiết có phần tử đơn vị, hay phần tử nghịch đảo như trong định nghĩa nhóm. Trong trường hợp này $(R, \times)$ gọi là **semigroup** (hay **nửa nhóm**).
````

````{prf:definition} Ring with identity, Vành với đơn vị
Nếu có phần tử $1_R \neq 0_R \in R$ sao cho với mọi $r \in R$ ta đều có

$$\begin{equation*}
    1_R \times r = r \times 1_R = r
\end{equation*}$$

thì $1_R$ được gọi là **phần tử đơn vị** đối với phép nhân.
````

Ta thường ký hiệu $0_R$ là phần tử đơn vị của phép cộng $(R, +)$ và gọi là **phần tử trung hòa**.

Khi đó phần tử nghịch đảo của phép cộng gọi là **phần tử đối** và được ký hiệu là $-a$, chỉ phần tử đối của phần tử $a$.

Ta ký hiệu $1_R$ là **phần tử đơn vị** đối với phép nhân $(R, \times)$.

Từ phần tử đơn vị đối với phép nhân ta có khái niệm **đặc số** (hay **số đặc trưng**, **characteristic**) của vành với đơn vị.

````{prf:definition} Characteristic, Đặc số
Xét trường $R$ với phần tử đơn vị là $1$ và phần tử trung hòa là 0. Số dương $p$ nhỏ nhất sao cho

$$\begin{equation*}
    \underbrace{1 + 1 + \ldots + 1 + 1}_{n \text{ lần}} = 0
\end{equation*}$$

được gọi là **đặc số** (hay **characteristic**) của $R$.
````

````{prf:definition} Commutative Ring, Vành giao hoán
Nếu ta có tính giao hoán đối với phép nhân, nghĩa là với mọi $a, b \in $ đều thỏa

$$\begin{equation*}
    a \times b = b \times a
\end{equation*}$$

thì ta nói là vành giao hoán.
````

### Trường

````{prf:definition} Field, Trường
Cho tập hợp $F$ và hai toán tử hai ngôi trên $F$ là phép cộng $+$ và phép nhân $\times$. Khi đó $(F, +, \times)$ là **trường** (hay **field**) nếu

1. $(F, +, \times)$ là vành giao hoán với đơn vị.
2. Với mọi phần tử $f \neq 0_F$, tồn tại nghịch đảo $f^{-1}$ của $f$ đối với phép nhân, nghĩa là $f \times f^{-1} = f^{-1} \times f = 1_F$
````

Nói cách khác, $(F, \times)$ là nhóm Abel. Trên trường ta thực hiện được bốn phép tính cộng, trừ, nhân, chia.

````{prf:example}
Các tập hợp sau với phép cộng và nhân là trường.

1. Tập hợp số thực $\mathbb{R}$.
2. Tập hợp các số phức $\mathbb{C}$.
3. Tập hợp các số dạng $a + b \sqrt{2}$ với $a, b \in \mathbb{Q}$.
````

Những trường trên được gọi là **trường vô hạn** vì có vô số phần tử.

Ngược lại, chúng ta cũng có các **trường hữu hạn**.

### Trường hữu hạn

#### Trường hữu hạn modulo nguyên tố

Cho $p$ là số nguyên tố. Khi đó tập hợp các số dư khi chia cho $p$ cùng với phép cộng và nhân modulo $p$ tạo thành trường.

```{admonition} **Chứng minh.**
:class: danger, dropdown
Xét tập hợp các số dư khi chia cho $p$ là $S = \{0, 1, \ldots, p-2, p-1\}$.

Ta thấy rằng với mọi $a, b \in S$ thì $a + b \pmod p$ và $a \cdot b \pmod p$ đều thuộc $S$.

1. Vì $0 + a = a + 0 = a \pmod p$ với mọi $a \in S$ nên $0$ là phần tử đơn vị của phép cộng.
2. Với mọi $a \in S$, ta có $(p-a) + a = a + (p-a) \equiv 0 \pmod p$ nên phần tử nghịch đảo của $a$ 
    đối với phép cộng là $p-a \in S$.
3. Phép cộng modulo có tính kết hợp
4. Phép cộng modulo có tính giao hoán

Như vậy $(S, +)$ là nhóm Abel.

Tiếp theo, ta thấy rằng phép cộng và nhân có tính phân phối trên modulo.
Đồng thời phép nhân modulo cũng có tính kết hợp. Do đó $(S, +, \cdot)$ là vành.

1. Phần tử đơn vị của phép nhân là 1
2. Phép nhân modulo có tính giao hoán
3. Do mọi phần tử thuộc $S$ đều nguyên tố cùng nhau với $p$ nên luôn tồn tại nghịch đảo của phần tử khác 0 trong $S$

Kết luận: $(S, +, \cdot)$ là trường.
```

Ta thường ký hiệu trường này là $\mathrm{GF}(p)$ (GF là viết tắt của Galois Field để tưởng nhớ người có đóng góp quan trọng trong lý thuyết nhóm).

#### Trường hữu hạn modulo đa thức

Xét các đa thức với hệ số nguyên

$$\begin{equation*}
    f(x) = a_n x^n + a_{n-1} x^{n-1} + \ldots + a_2 x^2 + a_1 x + a_0
\end{equation*}$$

Ta thấy rằng phép cộng và nhân hai đa thức tạo thành một vành giao hoán với đơn vị (đa thức $f(x) \equiv 1$).

Thêm nữa vành này có vô số phần tử. Ta cần một phương án để số phần tử là hữu hạn, và đồng thời là trường.

Với $p$ là số nguyên tố và $n$ là số nguyên dương. Mình xét các đa thức có bậc tối đa là $n-1$ với hệ số nằm trong tập hợp các số dư khi chia cho $p$. Như vậy mình có $p^n$ đa thức như vậy.

````{prf:example}
Với $p=3$ và $n=2$. Khi đó các đa thức có thể có là

$$\{ 0, 1, 2, x, x+1, x+2, 2x, 2x+1, 2x+2 \}$$
````

Tương tự với việc modulo cho một số nguyên tố, ở đây mình xét phép cộng và nhân trên modulo một đa thức tối giản (irreducible polynomial) có bậc $n$ (vì khi modulo một đa thức bậc bất kì cho đa thức bậc $n$ ta có đa thức bậc nhỏ hơn $n$). 

Đồng thời hệ số của đa thức từ phép cộng và nhân cũng được modulo $p$ (nằm trong $\mathrm{GF}(p)$).

Với trường hợp $p=3$ và $n=2$ ở trên mình có thể chọn đa thức modulo là $m(x) = x^2 + 2x + 2$. Sau đây bảng phép nhân (phép cộng khá đơn giản nên mình không viết) 2 đa thức bậc nhỏ hơn 2 trong modulo $m(x)$.

| | 0 | 1 | 2 | $x$ | $x+1$ | $x+2$ | $2x$ | $2x+1$ | $2x+2$ |
| - | - | - | - | - | - | - | - | - | - | 
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 1 | 2 | $x$ | $x+1$ | $x+2$ | $2x$ | $2x+1$ | $2x+2$ |
| 2 | 0 | 2 | 1 | $2x$ | $2x+2$ | $2x+1$ | $x$ | $x+2$ | $x+1$ |
| $x$ | 0 | $2x$ | $x+1$ | $2x$ | $2x+1$ | 1 | $2x+2$ | 2 | $x+2$ |
| $x+1$ | 0 | $x+1$ | $2x+2$ | $2x+1$ | 2 | $x$ | $x+2$ | $2x$ | 1 |
| $x+2$ | 0 | $x+2$ | $2x+1$ | 1 | $x$ | $2x+2$ | 2 | $x+1$ | $2x$ |
| $2x$ | 0 | $2x$ | $x$ | $2x+2$ | $x+2$ | 2 | $x+1$ | 1 | $2x+1$ |
| $2x+1$ | 0 | $2x+1$ | $x+2$ | 2 | $2x$ | $x+1$ | 1 | $2x+2$ | $x$ |
| $2x+2$ | 0 | $2x+2$ | $x+1$ | $x+2$ | 1 | $2x$ | $2x+1$ | $x$ | 2 |

Ta thấy rằng bảng phép nhân đối xứng qua đường chéo chính. Điều này chứng tỏ phép nhân có tính giao hoán. Thêm nữa ở mỗi hàng hoặc cột khác 0 đều có 9 phần tử khác nhau.

### Ideal

````{prf:definition} Ideal
Xét vành $(R, +, \times)$. Một tập con $I$ của $R$ được gọi là **ideal trái** nếu

1. $(I, +)$ là nhóm con của $(R, +)$.
2. Với mọi $r \in R$, với mọi $x \in I$ thì $rx \in I$.
````

Ta định nghĩa tương tự với ideal phải, khi đó $xr \in I$. Từ đây về sau nếu không nói gì thêm nghĩa là mình xét ideal trái.

````{prf:definition} Principal Ideal, Ideal chính
Nếu $I = aR$ với $a$ là phần tử nào đó trong $R$ thì $I$ được gọi là **principal ideal**.
````

Nói cách khác, nếu có một phần tử trong $R$ "sinh" ra được $I$ thì $I$ là principal.

````{prf:definition} Maximal Ideal, Ideal cực đại
Nếu $I$ là một ideal của $R$ và không tồn tại tập con $I'$ mà $I \subset I' \subset R$ (tập con thực thụ) thì $I$ được gọi là **maximal ideal**.
````

````{prf:remark}
Xét vành số nguyên $\mathbb{Z}$. Khi đó mọi ideal của $\mathbb{Z}$ đều là principal.
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
Giả sử ideal $I$ của $\mathbb{Z}$ có phần tử dương nhỏ nhất là $n$.

Theo định nghĩa của ideal thì với mọi $q \in \mathbb{Z}$ ta có  $qn \in I$.

Nếu phần tử $a \in I$, theo phép chia Euclid ta có $a = qn + r$ với $0 \leqslant r < n$, mà $a \in I$ và $qn \in I$ nên $r = a - qn \in I$.

Tuy nhiên phần tử dương nhỏ nhất thuộc $I$ là $n$, do đó $r = 0$.

Nói cách khác mọi phần tử $a \in I$ đều có dạng $qn$ với $q \in \mathbb{Z}$.

Vậy mọi ideal đều là principal.
```

````{prf:remark}
Ideal $I$ của $\mathbb{Z}$ là maximal khi và chỉ khi $I = n\mathbb{Z}$ với $n$ là số nguyên tố.
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
Ta chứng minh chiều thuận, chiều ngược tương tự. Sử dụng phản chứng, ta giả sử $n$ là hợp số. Khi đó $n = n_1 n_2$ ($n_1 \geqslant n_2 > 1$).

Khi đó $n \mathbb{Z} \subset n_1 \mathbb{Z} \subset \mathbb{Z}$, suy ra ideal không phải maximal. Ta có điều phải chứng minh.
```

````{prf:theorem}
Gọi $R$ là vành giao hoán với đơn vị. Khi đó, nếu $I$ là ideal của $R$ thì $R / I$ là trường khi và chỉ khi $I$ là maximal ideal.
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
Ta chứng minh điều kiện cần và điều kiện đủ.

**Điều kiện cần**. Ta có $I$ là maximal ideal. Ta thấy rằng $a + I \neq 0 \Leftrightarrow a \not\in I$. Vì nếu $a \in I$ thì tồn tại $-a \in I$. Theo định nghĩa vành thì $a R$ cũng là ideal nên $I + a R$ là ideal, mà $a \not\in I$ và $a \in I + a R$ suy ra $I \subset I + a R$. Ta lại có $I$ là maximal nên $I + aR = R$, do đó tồn tại $n \in I$ và $b \in R$ sao cho $n + ab = 1$. Tóm lại là tồn tại nghịch đảo của phép nhân, do đó $R / I$ là trường.

**Điều kiện đủ**. Với $R / I$ là trường. Ta giả sử $I$ không là maximal ideal. Khi đó tồn tại $I'$ sao cho $I \subset I' \subset R$.

Khi đó tồn tại phần tử $a \in I'$ và $a \not\in I$ mà $a + I \neq 0$. Do đó $(a + I) (b + I) = 1 + I$ suy ra tồn tại $n \in I \subset I'$ sao cho $a b = 1 + n$. Do $a, b \in I'$ nên $1 \in I'$, từ đó $1 \in R$ nên $I'$ không phải maximal.
```

````{prf:example}
Xét tập hợp $\mathbb{Z}$ là vành giao hoán với đơn vị. Khi đó nếu $n$ là số nguyên tố thì $n \mathbb{Z}$ là maximal ideal (đã chứng minh ở trên). Do đó tập $\mathbb{Z} / n\mathbb{Z}$ là trường hữu hạn modulo nguyên tố gồm các phần tử $\{ 0, 1, \ldots, p-1 \}$.
````

### Ring kernel và ring homomorphism

Xét vành $(R, +, \times)$. Khi đó:

- với mọi $a \in R$, $a \times 0 = 0 \times a = 0$;
- $(-a) \times b = - (a \times b)$.

````{prf:definition} Ring homomorphism
Xét hai vành là $(R_1, +, \times)$ và $(R_2, \boxplus, \otimes)$ và ánh xạ $f: \, R_1 \to R_2$.

Ánh xạ $f$ được gọi là **homomorphism** trên hai vành nếu $f$ là homomorphism trên phép cộng và phép nhân.

- với mọi $a, b \in R_1$, $f(a) \boxplus f(b) = f(a + b)$;
- với mọi $a, b \in R_1$, $f(a) \otimes f(b) = f(a \times b)$.
````

````{prf:definition} Kernel, Hạt nhân
**Hạt nhân** (hay **kernel**) của $f$ là

$$\begin{equation*}
    \ker f = \{x \vert x \in R_1, f(x) = 0_{2}\}
\end{equation*}$$

với $0_{2}$ là phần tử trung hòa của $R_2$.
````

````{prf:theorem}
$\ker f$ là một ideal của $R_1$.
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
Ta có $f(0_1) = 0_2$ theo định nghĩa homomorphism. Do đó với mọi $a \in R_1$ và với mọi $b \in \ker f$ thì $f(a) \otimes f(b) = f(a) \otimes 0_2 = 0_2 = f(a \times b)$. 

Do đó $a \times b \in \ker f$ nên suy ra $\ker f$ là ideal trái của $R_1$.

Tương tự cho với mọi $a \in R_1$ và với mọi $b \in \ker f$ thì $f(b) \otimes f(a) = 0_2 = f(b \times a)$. Suy ra $b \times a \in \ker f$ nên $\ker f$ cũng là ideal phải của $R_1$.

Kết luận: $\ker f$ là ideal của $R_1$.
```
