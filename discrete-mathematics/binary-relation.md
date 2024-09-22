# Quan hệ hai ngôi

```{contents}
:depth: 2
```

## Quan hệ hai ngôi

````{prf:definition} Quan hệ hai ngôi
Xét hai tập hợp $A$ và $B$. Ta gọi $\mathcal{R}$ là một quan hệ hai ngôi trên $A$ và $B$ nếu $\mathcal{R} \subset A \times B$. Trong đó $A \times B$ là tích Descartes của hai tập hợp.
````

Nếu phần tử $(a, b) \in R$ với $a \in A$ và $b \in B$ thì ta nói **$a$ có quan hệ với $b$** và ký hiệu $a \mathcal{R} b$.

Khi $A \equiv B$ thì ta nói $\mathcal{R}$ là quan hệ hai ngôi trên $A$. Đây cũng là yếu tố quan trọng cho các khái niệm về sau.

````{prf:example}
Xét hai tập hợp $A = \{1, 2, 3, 4\}$ và $B = \{a, b, c\}$. Khi đó tích Descartes 

$$\begin{align*}
    A \times B = \{
    & (1, a), (1, b), (1, c), (2, a), (2, b), (2, c), \\
    & (3, a), (3, b), (3, c), (4, a), (4, b), (4, c)
\}
\end{align*}$$

Giả sử $\mathcal{R} = \{(1, a), (3, b), (4, c)\}$ thì 1 quan hệ với $a$ do $(1, a) \in \mathcal{R}$, hay $1 R a$. Tuy nhiên 1 không có quan hệ với $b$ do $(1, b) \not\in \mathcal{R}$.
````

Sau đây ta định nghĩa các loại quan hệ hai ngôi.

````{prf:definition}
Cho $R$ là quan hệ hai ngôi trên tập $A$. Ta nói

1. $\mathcal{R}$ **phản xạ** (hay **reflexive**) nếu với mọi $x \in A$ thì $(x, x) \in \mathcal{R}$.
2. $\mathcal{R}$ **đối xứng** (hay **symmetric**) nếu $(x, y) \in \mathcal{R}$ thì $(y, x) \in \mathcal{R}$.
3. $\mathcal{R}$ **phản xứng** (hay **antisymmetric**) nếu $(x, y) \in \mathcal{R}$ thì $(y, x) \not\in \mathcal{R}$. Nói cách khác nếu $(x, y) \in \mathcal{R}$ và $(y, x) \in \mathcal{R}$ thì $x = y$.
4. $\mathcal{R}$ **bắc cầu** (hay **transitive**) nếu $(x, y) \in \mathcal{R}$ và $(y, z) \in \mathcal{R}$ thì $(x, z) \in \mathcal{R}$.
````

### Quan hệ tương đương

Quan hệ tương đương giúp ta chia (phân hoạch) một tập hợp rời rạc thành các tập con mà chỉ cần một phần tử đại diện cho tập con đó là đủ để tính toán.

````{prf:definition} Quan hệ tương đương
Cho $\mathcal{R}$ là quan hệ trên tập $A$. Khi đó $\mathcal{R}$ được gọi là **quan hệ tương đương** (hay **equivalence relation**, **отношение эквивалентности**) nếu $\mathcal{R}$ phản xạ, đối xứng và bắc cầu.

Ta có thể ký hiệu $x \mathcal{R} y$ với $\mathcal{R}$ là quan hệ tương đương là $x \sim y$ hoặc $x \widetilde{\mathcal{R}} y$.
````

Tiếp theo ta định nghĩa lớp tương đương chứa phần tử $x$ và tập thương.

````{prf:definition} Lớp tương đương
Cho $\mathcal{R}$ là quan hệ tương đương trên tập $A$. Khi đó với $x \in A$, ta định nghĩa lớp tương đương chứa phần tử $x$ là tập các phần tử của $A$ có quan hệ với $x$ 

$$\bar{x} = \{ y \in A, \, y \mathcal{R} x \}$$
````

````{prf:definition} Tập thương
Tập hợp các lớp tương đương như trên tạo thành tập thương.

$$A / \mathcal{R} = \{ \bar{x}, \, x \in A \}$$
````

````{prf:example}
Xét số nguyên dương $n$. Với số nguyên $x$ và $y$, ta nói $x$ có quan hệ với $y$ nếu $n \mid (x - y)$, hay $x \equiv y \bmod n$. Ta ký hiệu quan hệ này là $n \mathbb{Z}$.

Quan hệ trên là quan hệ tương đương vì

1. $n \mid 0 = x - x$ với mọi $x \in \mathbb{Z}$ nên có tính phản xạ.
2. $n \mid (x - y) \Rightarrow n \mid -(x-y) = y-x$  với mọi $x, y \in \mathbb{Z}$ nên có tính đối xứng.
3. $n \mid (x - y)$ và $n \mid (y - z)$ thì $n \mid (x - y + y - z) = (x - z)$ nên có tính bắc cầu.

Từ đó ta có thể phân tập $\mathbb{Z}$ thành các lớp tương đương

$$\begin{array}{ccl}
    \overline{0} & = & \{ \ldots, -2n, -n, 0, n, 2n, \ldots \} \\
    \overline{1} & = & \{ \ldots, -2n+1, -n+1, 1, n+1, 2n+1, \ldots \} \\
    \vdots \\
    \overline{n-1} & = & \{ \ldots, -n-1, -1, n-1, 2n-1, 3n-1, \ldots \}
\end{array}$$

Tập thương của chúng ta là $\mathbb{Z} / n\mathbb{Z} = \{ \overline{0}, \overline{1}, \ldots, \overline{n-1} \}$.
````

### Quan hệ thứ tự

````{prf:definition} Quan hệ thứ tự
Cho quan hệ $\mathcal{R}$ trên tập $A$. Ta nói $\mathcal{R}$ là **quan hệ thứ tự** (hay **order relation**, **отношение порядка**) nếu $\mathcal{R}$ phản xạ, phản xứng và bắc cầu.
````

````{prf:definition}
Cho tập hợp $A$ và quan hệ $\mathcal{R}$ trên $A$ là quan hệ thứ tự. Nếu $x \mathcal{R} y$ thì ta ký hiệu $x \prec y$. Khi đó $(A, \prec)$ được gọi là **tập có thứ tự** (hay **ordered set**).
````

Tiếp theo là một số định nghĩa quan trọng về tập hợp có thứ tự.

````{prf:definition}
Với $(A, \prec)$ và $x, y \in A$,

1. Nếu $x \prec y$, ta nói **$y$ là trội của $x$**, hay là **$x$ được trội bởi $y$**.
2. $y$ là **trội trực tiếp** của $x$ nếu không tồn tại $z$ sao cho $x \prec z$ và $z \prec y$.
````

````{prf:definition}
Xét $(A, \prec)$.

1. $x$ và $y$ thuộc $A$ được gọi là **so sánh được** nếu $x \prec y$ hoặc $y \prec x$.
2. Nếu với mọi $x, y \in A$, $x$ và $y$ so sánh được thì $(A, \prec)$ được gọi là **quan hệ thứ tự toàn phần**. Ngược lại thì gọi là **quan hệ thứ tự bán phần**.
````

Để biểu diễn sự so sánh trong một tập hợp, ta sử dụng biểu đồ Hasse.

````{prf:definition}
Biểu đồ Hasse của $(A, \prec)$ với $A$ là tập hữu hạn bao gồm

1. Tập điểm - mỗi điểm biểu diễn một phần tử của $A$.
2. Tập cung - vẽ một cung từ $x$ tới $y$ nếu $y$ là trội trực tiếp của $x$.
````

````{prf:example}
Xét tập $U_{12} = \{ 1, 2, 3, 4, 6, 12 \}$ với quan hệ $x \mathcal{R} y$ được định nghĩa $x$ là ước của $y$.

Theo đó, biểu đồ Hasse của quan hệ trên là {numref}`hasse:1`.

```{figure} ../figures/hasse/hasse.jpg
:name: hasse:1

Biểu đồ Hasse của $U_{12}$
```
````

````{prf:definition}
Xét quan hệ thứ tự $(A, \prec)$.

1. Phần tử $M \in A$ được gọi là
    1. **Tối đại** nếu $M \prec x$ thì $x = M$.
    2. **Cực đại** (hay **lớn nhất**) nếu với mọi $x \in A$ thì $x \prec M$.
2. Phần tử $m \in A$ được gọi là
    1. **Tối tiểu** nếu $x \prec m$ thì $x = m$.
    2. **Cực tiểu** (hay **nhỏ nhất**) nếu với mọi $x \in A$ thì $m \prec x$.
````

````{prf:remark}
1. Phần tử cực đại nếu có là duy nhất. Tương tự cho cực tiểu.
2. Nếu $n$ là phần tử tối đại duy nhất thì nó cũng là cực đại. Tương tự cho tối tiểu.
````

Trong ví dụ $U_{12}$ ở trên thì $1$ là tối tiểu và cũng là cực tiểu, và $12$ là tối đại và cũng là cực đại.
