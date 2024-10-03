## Hàm affine và hàm tuyến tính

### Hàm affine và hàm tuyến tính

````{prf:definition} Hàm boolean affine
Xét hàm boolean $n$ biến $f(x_1, x_2, \ldots, x_n)$. Khi đó $f$ được gọi là **hàm boolean affine** nếu nó có dạng

$$\begin{equation}
    f(x_1, x_2, \ldots, x_n) = a_0 \oplus a_1 x_1 \oplus 
    a_2 x_2 \oplus \ldots \oplus a_n x_n
\end{equation}$$

Khi $a_0 = 0$ thì ta gọi là **hàm boolean tuyến tính** (linear).
````

Ta thấy rằng chỉ có các hạng tử dạng $a_i x_i$ xuất hiện trong biểu diễn đa thức Zhegalkin tương ứng của hàm boolean đó. Hay  nói cách khác hàm boolean là affine khi $\deg(f) = 1$.

````{prf:example}
Hàm boolean $f(x, y) = x \oplus y$ là hàm boolean affine và cũng tuyến tính. Hàm boolean $f(x, y) = x \oplus xy$ không là hàm boolean affine.
````

### Số lượng hàm affine và hàm tuyến tính

Ở phần trên ta đã tính được

$$\lvert \mathcal{F}_n \rvert = 2^{2^n}.$$

Số lượng hàm boolean affine là số cách chọn các hệ số $a_0$, $a_1$, ..., $a_n$. Như vậy cần chọn $n+1$ số trong $\mathbb{F}_2$ nên

$$\lvert \mathcal{A}_n \rvert = 2^{n+1}.$$

Đối với hàm boolean tuyến tính thì chọn từ $a_1$ tới $a_n$ nên cần chọn $n$ số, suy ra

$$\lvert \mathcal{L}_n \rvert = 2^n.$$