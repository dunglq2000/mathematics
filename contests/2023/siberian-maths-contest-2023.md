## Siberian Mathematical Contest 2023

### Đề dành cho năm nhất

#### Bài 1

##### Đề bài

Tồn tại hay không một đa thức $p(x)$ sao cho mọi hệ số khác không của nó không phải số nguyên, nhưng với hai số nguyên bất kì khác nhau $a$ và $b$ ta đều có $\dfrac{p(a) - p(b)}{b - a}$ là số nguyên?

##### Lời giải

Tồn tại, ví dụ như $p(x) = \dfrac{x^4 + x^2}{2}$:

$$\frac{p(a) - p(b)}{a - b} = \cdots = \frac{(a + b)(a^2 + b^2 + 1)}{2}$$

Vì $a+b$ và $a^2 + b^2 + 1$ khác tính chẵn lẻ nên tích trên luôn chia hết cho $2$ và do đó là số nguyên.

#### Bài 2

##### Đề bài

Cho dãy $\{ a_n \}$, $n \geqslant 0$ thỏa điều kiện $a_0 = 1$, $a_1 = \dfrac{1}{2}$,

$$a_n = \frac{n}{2} a_{n-1} + \frac{n(n-1)}{2} a_{n-2} + \frac{(-1)^n (1 - n)}{2(n+1)}$$

Tìm $\lim\limits_{n \to \infty} \dfrac{a_n}{n!}$.

##### Lời giải

Từ quy nạp toán học có thể tìm được

$$a_n = n a_{n-1} + \frac{(-1)^n}{n+1}$$

Từ đó,

$$\begin{align*}
    a_n & = n \left( (n-1) a_{n-2} + \frac{(-1)^{n-1}}{n} \right) + \frac{(-1)^n}{n+1} \\
    & = n (n-1) a_{n-2} + (-1)^{n-1} + \frac{(-1)^n}{n+1} \\
    & = \ldots \\
    & = n! a_0 - \frac{n!}{2!} + \frac{(-1)^2 n!}{3!} + \frac{(-1)^3 n!}{4!} + \cdots + \frac{(-1)^{n-1} n!}{n!} + \frac{(-1)^n n!}{n!} 
\end{align*}$$

Nói cách khác,

$$\begin{align*}
    \frac{a_n}{n!} & = a_0 + \frac{(-1)^1}{2!} + \frac{(-1)^2}{3!} + \frac{(-1)^3}{4!} + \cdots + \frac{(-1)^{n-1}}{n!} + \frac{(-1)^n}{n!} \\
    & = \sum_{k=0}^n \frac{(-1)^k}{(k+1)!} = 1 - \sum_{k=0}^{n+1} \frac{(-1)^k}{k!} \to 1 - \frac{1}{e}
\end{align*}$$

#### Bài 3

##### Đề bài

Cho hàm đơn điệu liên tục tăng nghiêm ngặt $f(x)$ xác định trên nửa khoảng $[0, +\infty)$ và thỏa $f(0) = 0$. Đặt $g(x)$ là hàm ngược của $f(x)$. Chứng minh rằng, với mọi số nguyên $m, n$ thì bất đẳng thức sau thỏa mãn:

$$m n \leqslant \sum_{k=0}^m [f(k)] + \sum_{s=0}^n [g(s)]$$

##### Lời giải

Giả sử, $[f(m)] \geqslant n$. Đặt $[f(s)] = l_s$. Theo tính đơn điệu thì $l_s \leqslant f(s) < l_{s+1}$. Do $f(x)$ liên tục và đơn điệu tăng nghiêm ngặt nên $g(x)$ cũng liên tục và đơn điệu.

$$\sum_{k=0}^m [f(k)] = l_1 + l_2 + \cdots + l_m;$$

$$\sum_{s=0}^n [g(s)] = 1 (l_2 - l_1) + 2(l_3 - l_2) + 3 (l_4 - l_3) + \cdots + p(n - l_p)$$

với $p$ nào đó mà $l_p < n \leqslant l_{p+1}$. Từ đây ta có

$$l_1 + l_2 + \cdots + l_p + 1 (l_2 - l_1) + 2 (l_3 - l_2) + \cdots + (p-1) (l_p - l_{p-1}) = p l_p$$

Vì $l_{p+1}, l_{p+2}, \ldots, l_m > n$ nên

$$\begin{align*}
\sum_{k=0}^m [f(k)] + \sum_{s=0}^n [g(s)] & = p l_p + p(n - l_p) + l_{p+1} + l_{p+2} + \cdots + l_m \\
& = pn + l_{p+1} + l_{p+2} + \cdots + l_m > pn + (m - p) n = mn.
\end{align*}$$

Chứng minh tương tự cho $[f(m)] < n$ (thay $f(x)$ thành $g(x)$).

#### Bài 4

##### Đề bài

Cho đa thức với hệ số nguyên

$$f(x) = x^{2m} + x^{m+2} - 4 x^m + x^{m-n} + 1$$

với $m > n$ là hai số tự nhiên nguyên tố cùng nhau. Tìm ước chung lớn nhất giữa $f(x)$ và $f'(x)$.

##### Lời giải

Ta thấy rằng $x=1$ là nghiệm bậc hai của $f(x)$. Ta sẽ chứng minh rằng $f(x)$ và $f'(x)$ không có nghiệm tổng quát (nghiệm phức) nào khác. Giả sử có nghiệm $z \in \mathbb{C}$. Khi đó

$$z^m + z^{-m} + z^n + z^{-n} = 4, m(z^m - z^{-m}) + n(z^n - z^{-n}) = 0$$

Đặt $u = z^m$ và $v = z^n$. Khi đó

$$u + u^{-1} + v + v^{-1} = 4, m (u - u^{-1}) + n (v - v^{-1}) = 0$$

Nếu $u$ và $v$ bằng $1$ thì $z = 1$ vì $(m, n) = 1$. Nếu $u \neq 1$ và $v \neq 1$ thì ta nghiệm của hệ phương trình là $(u, v) \in \{ (u_0, v_0), (u_0^{-1}, v_0^{-1}) \}$ với

$$u_0 = - \frac{m^2 + 3n^2 + 2n \sqrt{2(m^2 + n^2)}}{m^2 - n^2}, v_0 = \frac{3m^2 + n^2 + 2m \sqrt{2 (m^2 + n^2)}}{m^2 - n^2}$$

Ở đây $u_0$ và $v_0$ là các số thực và thỏa mãn đẳng thức $u_0^n = v_0^m$. Nhưng vì $1 < \lvert u_0 \rvert < v_0$ nên khi $m > n$ các đẳng thức trên không đúng.

