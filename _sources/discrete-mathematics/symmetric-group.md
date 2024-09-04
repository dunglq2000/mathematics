## Nhóm hoán vị

```{contents}
```

### Nhóm hoán vị

Xét tập hợp $\{ 1, 2, \ldots, n \}$. Ta gọi $\mathcal{S}_n$ là tập tất cả hoán vị của tập hợp trên. Như vậy $\mathcal{S}_n$ có $n!$ phần tử.

Nếu ta lấy hoán vị gốc là $(1, 2, \ldots n)$, mỗi hoán vị đều có thể được biểu diễn bằng hai hàng như sau:

$$\begin{equation*}
    \sigma = \begin{pmatrix}
        1 & 2 & \ldots & n \\
        \sigma(1) & \sigma(2) & \ldots & \sigma(n)
    \end{pmatrix}
\end{equation*}$$

Ta định nghĩa toán tử trên $\mathcal{S}_n$. Với hai hoán vị $\sigma$ và $\tau$, hoán vị $\sigma \star \tau$ là vị trí của $\sigma$ theo $\tau$. Nói cách khác, nếu

$$\begin{equation*}
    \sigma = \begin{pmatrix}
    1 & 2 & \ldots & n \\
    \sigma(1) & \sigma(2) & \ldots & \sigma(n)
\end{pmatrix}
\end{equation*}$$

và 

$$\begin{equation*}
    \tau = \begin{pmatrix}
    1 & 2 & \ldots & n \\
    \tau(1) & \tau(2) & \ldots & \tau(n)
\end{pmatrix}
\end{equation*}$$

thì 

$$\begin{equation*}
    \sigma \star \tau =
\begin{pmatrix}
    1 & 2 & \ldots & n \\
    \sigma(\tau(1)) & \sigma(\tau(2)) & \ldots & \sigma(\tau(n))   
\end{pmatrix}
\end{equation*}$$

Nhóm $\mathcal{S}_n$ và toán tử như trên tạo thành một nhóm và được gọi là **nhóm hoán vị**.

````{prf:example}
Xét nhóm hoán vị $\mathcal{S}_5$. 

Gọi $x = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 4 & 3 & 1 & 2 & 5
\end{pmatrix}$ và
$y = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 5 & 1 & 4 & 3 & 2
\end{pmatrix}$. Khi đó, đặt $z = x \star y$ thì

$$\begin{align*}
    & z(1) = x(y(1)) = x(5) = 5, \\
    & z(2) = x(y(2)) = x(1) = 4, \\
    & z(3) = x(y(3)) = x(4) = 2, \\
    & z(4) = x(y(4)) = x(3) = 1, \\ 
    & z(5) = x(y(5)) = x(2) = 3
\end{align*}$$

Như vậy $z = x \star y = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 5 & 4 & 2 & 1 & 3
\end{pmatrix}$.
````

````{prf:remark}
Trong một hoán vị, khi biểu diễn trên hai hàng thì thứ tự viết không quan trọng, miễn là đảm bảo $i$ tương ứng với $\sigma(i)$ trên từng cột.
````

````{prf:example}
Xét hoán vị $\sigma = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 4 & 3 & 1 & 2 & 5
\end{pmatrix}$ thuộc $\mathcal{S}_5$.

Ta có $\sigma(1) = 4$, $\sigma(2) = 3$, $\sigma(3) = 1$, $\sigma(4) = 2$
và $\sigma(5) = 5$. Như vậy hai cách viết sau là giống nhau

$$\begin{equation*}
    \sigma = 
    \begin{pmatrix}
        1 & 2 & 3 & 4 & 5 \\
        4 & 3 & 1 & 2 & 5
    \end{pmatrix} = 
    \begin{pmatrix}
        3 & 4 & 5 & 1 & 2 \\
        1 & 2 & 5 & 4 & 3
    \end{pmatrix}
\end{equation*}$$
````

### Chu trình độc lập

Xét nhóm hoán vị $\mathcal{S}_n$ và hoán vị $\sigma$ thuộc $\mathcal{S}_n$.

Khi đó tồn tại các tập $\{ i_1, i_2, \ldots, i_k \} \subset \{1, 2, \ldots, n\}$
sao cho $\sigma(i_1) = i_2$, $\sigma(i_2) = i_3$, ..., $\sigma(i_{k-1})
= \sigma(i_k)$ và $\sigma(i_k) = i_1$.

````{prf:example}
Xét $\mathcal{S}_5$ và hoán vị $\sigma = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 5 & 1 & 4 & 3 & 2
\end{pmatrix}$. 

Ta thấy rằng $\sigma(1) = 5$, $\sigma(5) = 2$,
$\sigma(2) = 1$. Như vậy ta có chu trình $1 \to 5 \to 2 \to 1$.

Tương tự, $\sigma(3) = 4$ và $\sigma(4) = 3$. Như vậy ta
có thêm chu trình $3 \to 4 \to 3$.

Hai chu trình trên không chứa phần tử chung nên chúng được gọi là
hai **chu trình độc lập**.
````

````{prf:remark}
Mọi hoán vị đều có thể viết được dưới dạng tích của các chu trình độc lập. **Chu trình có thể chứa một phần tử** ($\sigma(i) = i$).
````

````{prf:example}
Hoán vị $\sigma = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 5 & 1 & 4 & 3 & 2
\end{pmatrix}$ như trên thì ta có thể viết lại thành $\sigma = (1, 5, 2)(3, 4)$.
````

````{prf:remark}
Thứ tự của chu trình trong tích không quan trọng. Điều này dễ thấy vì các chu trình độc lập nhau, do đó dù viết trước hay sau thì hoán vị vẫn nằm trong chu trình đó.
````

Để giải thích rõ hơn, chúng ta có thể xem mỗi chu trình độc lập như một hoán vị, trong đó các phần tử không thuộc chu trình đứng yên. 

Ví dụ với chu trình $(1, 5, 2) = (1, 5, 2)(3)(4)$
ở trên tương đương với

$$p_1 = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 5 & 1 & 3 & 4 & 2
\end{pmatrix}$$

và với chu trình $(3, 4) = (3, 4)(1)(2)(5)$ tương đương với

$$p_2 = \begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 1 & 2 & 4 & 3 & 5
\end{pmatrix} = \begin{pmatrix}
    5 & 1 & 3 & 4 & 2 \\ 5 & 1 & 4 & 3 & 2
\end{pmatrix}$$

Do đó tích của chúng (hay toán tử trên nhóm hoán vị) sẽ cho ra kết quả hoán vị ban đầu.

$$\underbrace{\begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 5 & 1 & 4 & 3 & 2
\end{pmatrix}}_{\sigma} = \underbrace{\begin{pmatrix}
    1 & 2 & 3 & 4 & 5 \\ 5 & 1 & 3 & 4 & 2
\end{pmatrix}}_{p_1} \star \underbrace{\begin{pmatrix}
    5 & 1 & 3 & 4 & 2 \\ 5 & 1 & 4 & 3 & 2 
\end{pmatrix}}_{p_2}$$
