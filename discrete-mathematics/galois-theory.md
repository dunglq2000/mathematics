# Lý thuyết Galois

```{contents}
:depth: 2
```

Tài liệu tham khảo trong phần này lấy từ sách {cite}`Judson2012` và trang youtube {cite}`Macauley61`.

## Extension Fields

### Extension Fields

````{prf:definition} Mở rộng trường
Trường $E$ được gọi là **mở rộng trường** (hay **extension field**) của trường $F$ nếu $F$ là trường con của $E$. Khi đó $F$ được gọi là **trường cơ sở** (hay **base field**) và ký hiệu $F \subset E$.
````

````{prf:example}
Trường nào nhỏ nhất chứa $\mathbb{Q}$ và $\sqrt{2}$?

Đáp án là trường $\mathbb{Q}(\sqrt{2}) = \{ a + b \sqrt{2} : a, b \in \mathbb{Q} \}$.

Việc chứng minh $\mathbb{Q}(\sqrt{2})$ là trường khá đơn giản, phần tử nghịch đảo đối với phép nhân của $a + b \sqrt{2}$ là

$$\begin{equation*}
    \frac{a}{a^2 - 2 b^2} + \frac{-2b}{a^2 - 2 b^2} \sqrt{2}
\end{equation*}$$
````

````{prf:example}
Trường nào nhỏ nhất chứa $\mathbb{Q}$ và $i$ (ở đây $i$ là đơn vị ảo, $i^2 = -1$)?

Đáp án là trường $\mathbb{Q}(i) = \{ a + b i : a, b \in \mathbb{Q} \}$. Tương tự, ở đây phần tử nghịch đảo đối với phép nhân của $a + b i$ là

$$\begin{equation*}
    \frac{a}{a^2 + b^2} + \frac{-b}{a^2 + b^2} i
\end{equation*}$$
````

Ở đây $\mathbb{Q}(\sqrt{2})$ và $\mathbb{Q}(i)$ đều là mở rộng của $\mathbb{Q}$ và đều là tập con của $\mathbb{C}$. Tuy nhiên hai trường này không phải tập con của nhau.

Như vậy, bằng việc mở rộng $\mathbb{Q}$ với $\sqrt{2}$ ta có trường $\mathbb{Q}(\sqrt{2})$.

Tương tự, bằng việc mở rộng $\mathbb{Q}$ với $i$ ta có trường $\mathbb{Q}(i)$.

Vậy trường nào chứa $\mathbb{Q}$, $\sqrt{2}$ và $i$?

````{prf:example}
Trường chứa cả $\mathbb{Q}$, $\sqrt{2}$ và $i$ là tập hợp

$$\begin{equation*}
    \mathbb{Q}(\sqrt{2}, i) = \{ a + b\sqrt{2} + c i + d \sqrt{2} i : a, b, c, d \in \mathbb{Q} \}
\end{equation*}$$
````

Trường trên có thể suy ra từ logic sau. Ta đã có $\mathbb{Q}(i)$ chứa $\mathbb{Q}$ và $i$. Ta muốn thêm $\sqrt{2}$ vào trường $\mathbb{Q}(i)$ nên ta sẽ muốn mở rộng $\mathbb{Q}(i)$ lên $\mathbb{Q}(i)(\sqrt{2})$.

Khi đó $\mathbb{Q}(i)(\sqrt{2})$ tương tự sẽ có dạng

$$\begin{equation*}
    \mathbb{Q}(i)(\sqrt{2}) = \{ \alpha + \beta \sqrt{2} : \alpha, \beta \in \mathbb{Q}(i) \}
\end{equation*}$$

Nói cách khác $\alpha = a + b i$ và $\beta = c + d i$, $a, b, c, d \in \mathbb{Q}$, nên ta có

$$\begin{equation*}
    \alpha + \beta \sqrt{2} = a + b i + c \sqrt{2} + d \sqrt{2} i, \quad a, b, c, d \in \mathbb{Q}
\end{equation*}$$

Khi đó ta viết

$$\begin{equation*}
    \mathbb{Q}(i)(\sqrt{2}) = \mathbb{Q}(\sqrt{2}, i) = \{ a + b\sqrt{2} + c i + d \sqrt{2} i : a, b, c, d \in \mathbb{Q} \}
\end{equation*}$$

````{prf:remark}
1. $\mathbb{Q}(\sqrt{2})$ là trường con của $\mathbb{R}$ nhưng $\mathbb{Q}(i)$ không phải.
2. $\mathbb{Q}(i)$ nhỏ hơn $\mathbb{C}$ rất nhiều (không chứa $\sqrt{2}$).
3. $\mathbb{Q}(\sqrt{2})$ chứa tất cả nghiệm của đa thức $f(x) = x^2 - 2$ trên $\mathbb{Q}$. Do đó $\mathbb{Q}(\sqrt{2})$ được gọi là **trường phân rã** của đa thức $f(x)$.
````

### Biểu diễn quan hệ giữa các trường qua lattice

Ở phần trước, $\mathbb{Q}(\sqrt{2})$ là mở rộng của $\mathbb{Q}$ và với hai phần tử $a, b \in \mathbb{Q}$ xác định một phần tử $a + b \sqrt{2} \in \mathbb{Q}(\sqrt{2})$.

Do $a + b \sqrt{2} = a \cdot 1 + b \cdot \sqrt{2}$ nên $\{ 1, \sqrt{2} \}$ là **cơ sở** (hay **basis**) của $\mathbb{Q}(\sqrt{2})$. Cơ sở chứa hai phần tử nên ta nói **bậc của mở rộng đơn** (hay **degree**) từ $\mathbb{Q}$ lên $\mathbb{Q}(\sqrt{2})$ là 2.

Tương tự, mở rộng từ $\mathbb{Q}$ lên $\mathbb{Q}(i)$ cũng có bậc là 2 với cơ sở là $(1, i)$.

Như vậy ta cũng các trường $\mathbb{Q}(\sqrt{2})$, $\mathbb{Q}(\sqrt{3})$ và $\mathbb{Q}(\sqrt{6})$ là các mở rộng đơn bậc 2 của $\mathbb{Q}$ ({numref}`extension_field-1`).

```{figure} ../figures/extension_field-1.jpg
:name: extension_field-1

Mở rộng trường $\mathbb{Q}$ lên $\mathbb{Q}(\sqrt{2})$, $\mathbb{Q}(\sqrt{3})$ và $\mathbb{Q}(\sqrt{6})$
```

Do $\sqrt{6} = \sqrt{2} \cdot \sqrt{3}$ dẫn ta tới câu hỏi, trường nào nhỏ nhất chứa cả $\sqrt{2}$ và $\sqrt{3}$?

Thực hiện tương tự với $\mathbb{Q}(\sqrt{2}, i)$ ở trên ta có trường

$$\begin{equation*}
    \mathbb{Q}(\sqrt{2}, \sqrt{3}) = \mathbb{Q}(\sqrt{2})(\sqrt{3}) = \{ a + b \sqrt{2} + c \sqrt{3} + d \sqrt{6} : a, b, c, d \in \mathbb{Q} \}
\end{equation*}$$

là trường nhỏ nhất chứa cả $\sqrt{2}$ và $\sqrt{3}$.

Ở đây, $\mathbb{Q}(\sqrt{2}, \sqrt{3})$ là mở rộng bậc 4 của $\mathbb{Q}$ với cơ sở là $\{ 1, \sqrt{2}, \sqrt{3}, \sqrt{6} \}$.

Bằng việc mở rộng từ $\mathbb{Q}(\sqrt{2})$ lên $\mathbb{Q}(\sqrt{2}, \sqrt{3}) = \mathbb{Q}(\sqrt{2})(\sqrt{3})$ ta cũng có đây là mở rộng bậc 2 (tương tự chứng minh phía trên cho $\mathbb{Q}(\sqrt{2}, i)$). Như vậy mở rộng từ $\mathbb{Q}(\sqrt{3})$ lên $\mathbb{Q}(\sqrt{2}, \sqrt{3})$ cũng là mở rộng bậc 2.

Vậy mở rộng từ $\mathbb{Q}(\sqrt{6})$ lên $\mathbb{Q}(\sqrt{2}, \sqrt{3})$ là bậc mấy? Để xác định ta cần chứng minh nhận xét sau

````{prf:remark}
$\mathbb{Q}(\sqrt{2}, \sqrt{3}) \equiv \mathbb{Q}(\sqrt{2} + \sqrt{3})$, trong đó $\mathbb{Q}(\sqrt{2} + \sqrt{3})$ là trường nhỏ nhất chứa $\mathbb{Q}$ và $\sqrt{2} + \sqrt{3}$.
````

```{admonition} **Chứng minh**
:class: danger, dropdown

Ta chứng minh $\mathbb{Q}(\sqrt{2}, \sqrt{3}) \subset \mathbb{Q}(\sqrt{2} + \sqrt{3})$.

Do $\sqrt{2} + \sqrt{3}$ nên nghịch đảo $\dfrac{1}{\sqrt{2} + \sqrt{3}} = \sqrt{3} - \sqrt{2} \in \mathbb{Q}(\sqrt{2} + \sqrt{3})$.

Khi đó, $\dfrac{1}{2} \cdot (\sqrt{2} + \sqrt{3}) \pm \dfrac{1}{2} \cdot (\sqrt{3} - \sqrt{2}) \in \mathbb{Q}(\sqrt{2} + \sqrt{3})$.

Vế trái sẽ bằng $\sqrt{2}$ hoặc $\sqrt{3}$. Như vậy $\sqrt{2}, \sqrt{3} \in \mathbb{Q}(\sqrt{2} + \sqrt{3})$.

Phép nhân trên trường cho ta $\sqrt{2} \cdot \sqrt{3} = \sqrt{6} \in \mathbb{Q}(\sqrt{2} + \sqrt{3})$.

Như vậy với mọi $a, b, c, d \in \mathbb{Q}$ ta có $a + b \sqrt{2} + c \sqrt{3} + d \sqrt{6} \in \mathbb{Q}(\sqrt{2} + \sqrt{3})$. Điều này tương đương với $\mathbb{Q}(\sqrt{2}, \sqrt{3}) \subset \mathbb{Q}(\sqrt{2} + \sqrt{3})$.

Nhưng mà $\mathbb{Q}(\sqrt{2} + \sqrt{3})$ là trường nhỏ nhất chứa $\mathbb{Q}$ và $\sqrt{2} + \sqrt{3}$, và $\mathbb{Q}(\sqrt{2}, \sqrt{3})$ là trường nhỏ nhất chứa $\sqrt{2}$ và $\sqrt{3}$, kéo theo chứa cả $\sqrt{2} + \sqrt{3}$ nên $\mathbb{Q}(\sqrt{2} + \sqrt{3}) \equiv \mathbb{Q}(\sqrt{2}, \sqrt{3})$.
```

Ta có $\mathbb{Q}(\sqrt{6}) = \{ a + b \sqrt{6} : a, b \in \mathbb{Q} \}$. Khi đó

$$\begin{equation}
    \mathbb{Q}(\sqrt{6})(\sqrt{2} + \sqrt{3}) = \{ \alpha + \beta (\sqrt{2} + \sqrt{3}) : \alpha, \beta \in \mathbb{Q}(\sqrt{6}) \}
\end{equation}$$ (QQ6_to_QQ2+3)

Đặt $\alpha = a + b \sqrt{6}$ và $\beta = c + d \sqrt{6}$, như vậy mỗi phần tử trong $\mathbb{Q}(\sqrt{6})(\sqrt{2} + \sqrt{3})$ có dạng

$$\begin{align*}
    a + b \sqrt{6} + (c + \sqrt{6})(\sqrt{2} + \sqrt{3}) = & a + (c + 3d) \sqrt{2} + (c + 2d) \sqrt{3} + b \sqrt{6} \\
        = & a' + b' \sqrt{2} + c' \sqrt{3} + d' \sqrt{6}
\end{align*}$$

với $a \to a'$, $c+3d \to b'$, $c + 2d \to c'$ và $b \to d'$.

Biến đổi này tương đương với hệ phương trình tuyến tính

$$\begin{equation*}
    \begin{pmatrix}
        1 & 0 & 0 & 0 \\
        0 & 0 & 1 & 3 \\
        0 & 0 & 1 & 2 \\
        0 & 1 & 0 & 0
    \end{pmatrix} \begin{pmatrix}
        a \\ b \\ c \\ d
    \end{pmatrix} = \begin{pmatrix}
        a' \\ b' \\ c' \\ d'
    \end{pmatrix}
\end{equation*}$$

Ma trận trên khả nghịch trên $\mathbb{Q}$, do đó $\mathbb{Q}(\sqrt{6})(\sqrt{2} + \sqrt{3}) \equiv \mathbb{Q}(\sqrt{2}, \sqrt{3})$. Ở dạng biểu diễn {eq}`QQ6_to_QQ2+3` ta suy ra mở rộng từ $\mathbb{Q}(\sqrt{6})$ lên $\mathbb{Q}(\sqrt{2}, \sqrt{3})$ là mở rộng bậc 2.

Sơ đồ mở rộng trường bây giờ như sau

```{figure} ../figures/extension_field-2.jpg
```

### Splitting Field

````{prf:definition} Trường phân rã
Xét trường $F$ và đa thức khác hằng $p(x) = a_n x^n + a_{n-1} x^{n-1} + \ldots + a_1 x + a_0$ trên $F[x]$ ($a_i \in F$ với mọi $i = 1, 2, \ldots$).

Trường mở rộng $E$ của trường $F$ được gọi là **trường phân rã** (hay **splitting field**) của $p(x)$ nếu tồn tại các phần tử $\alpha_1, \alpha_2, \ldots, \alpha_n$ thuộc $E$ sao cho $E = F(\alpha_1, \alpha_2, \ldots, \alpha_n)$ và

$$\begin{equation*}
    p(x) = (x - \alpha_1) (x - \alpha_2) \cdots (x - \alpha_n)
\end{equation*}$$
````

Khi đó ta nói đa thức $p(x) \in F[x]$ phân rã (split) trong $E$ nếu nó phân tích thành các nhân tử bậc nhất (tuyến tính) trong $E[x]$.

Nói nôm na, nếu đa thức có hệ số trong một trường $F$ nào đó (tức thuộc $F[x]$) thì các nghiệm của nó nằm trong một trường lớn hơn chứa $F$.

````{prf:example}
Đa thức $f(x) = x^2 - 2$ trên $\mathbb{Q}[x]$ không có nghiệm trên $\mathbb{Q}$. Tuy nhiên $\mathbb{Q}(\sqrt{2})$ là trường chứa $\mathbb{Q}$ và các nghiệm của $f(x)$ là $\pm \sqrt{2}$. Vì vậy $\mathbb{Q}(\sqrt{2})$ là trường phân rã của $f(x)$.
````

````{prf:example}
Đa thức $g(x) = x^2 + 1$ trên $\mathbb{Q}[x]$ không có nghiệm trên $\mathbb{Q}$. Tuy nhiên $g(x)$ có hai nghiệm là $\pm i$ và $\mathbb{Q}(i)$ chứa cả $\mathbb{Q}$ và $\pm i$ nên $\mathbb{Q}(i)$ là một trường phân rã của $g(x)$.
````

Ở đây, bậc của đa thức $f(x) = x^2 - 2$ bằng với bậc của mở rộng trường từ $\mathbb{Q}$ lên $\mathbb{Q}(\sqrt{2})$.

Tương tự, bậc của mở rộng trường từ $\mathbb{Q}$ lên $\mathbb{Q}(\sqrt{3})$ bằng bậc đa thức $g(x) = x^2 - 3$, và bậc của mở rộng trường từ $\mathbb{Q}$ lên $\mathbb{Q}(\sqrt{6})$ bằng với bậc đa thức $h(x) = x^2 - 6$.

Ở trên ta đã chứng minh bậc của mở rộng trường từ $\mathbb{Q}(\sqrt{2})$ lên $\mathbb{Q}(\sqrt{2}, \sqrt{3})$ là 2, điều này tương ứng với bậc của đa thức $k(x) = (x^2 - 2)(x^2 - 3) = x^4 - 5 x + 6$.

Tổng kết lại, nếu $E$ là trường phân rã của $F$ trên đa thức $f(x) \in F[x]$ thì bậc của mở rộng trường từ $F$ lên $E$ bằng với bậc của $f(x)$.

Từ sơ đồ mở rộng trường bên trên ta có sơ đồ với đa thức tương ứng.

```{figure} ../figures/extension_field-3.jpg
```

Vậy còn mở rộng từ $\mathbb{Q}(\sqrt{6})$ thành $\mathbb{Q}(\sqrt{2}, \sqrt{3})$? Ở trên ta đã chứng minh rằng đây là mở rộng bậc 2. Vậy chúng ta cần tìm một đa thức bậc 2 có hệ số trong $\mathbb{Q}(\sqrt{6})$ mà không có nghiệm trong $\mathbb{Q}(\sqrt{6})$.

Quay lại một chút, ta đã mở rộng $\mathbb{Q}(\sqrt{6})$ lên $\mathbb{Q}(\sqrt{2}, \sqrt{3})$ với sự trợ giúp của phần tử $\sqrt{2} + \sqrt{3}$. Từ đây ta có thể xây dựng đa thức

$$\begin{equation*}
    m(x) = x^2 - (\sqrt{2} + \sqrt{3})^2 = x^2 - 5 - 2 \sqrt{6}
\end{equation*}$$

Đa thức $m(x)$ có hệ số trong $\mathbb{Q}(\sqrt{6})$ nhưng không có nghiệm trong $\mathbb{Q}(\sqrt{6})$ mà trong $\mathbb{Q}(\sqrt{2}, \sqrt{3})$. Ta có điều phải chứng minh.
