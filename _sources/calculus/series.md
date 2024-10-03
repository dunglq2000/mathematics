# Chuỗi số

Xét dãy số $\{a_n\}$. Đặt

$$S_n = a_1 + a_2 + \ldots + a_n$$

Khi đó $\{S_n\}$ là chuỗi số. Tương tự như sự hội tụ hoặc phân kỳ của dãy số, ta cũng quan tâm đến sự hội tụ và phân kỳ của chuỗi số.

````{prf:definition} Chuỗi số hội tụ
Chuỗi số $\{S_n\}$ được gọi là **hội tụ** nếu tồn tại giới hạn hữu hạn $\displaystyle{L = \lim_{n \to \infty} S_n}$.
````

Ngược lại ta gọi là chuỗi phân kỳ. Nghĩa là $\displaystyle{\lim_{n \to \infty} S_n = \infty}$ hoặc không tồn tại $\lim\limits_{n \to \infty} S_n$.

````{prf:example}
Xét dãy số $a_n = \dfrac{1}{2^n}$ với $n = 1, 2, \ldots$.

Khi đó

$$\begin{align*}
    S_n & = \frac{1}{2} + \frac{1}{2^2} + \ldots + \frac{1}{2^n} \\
    & = \frac{1}{2} \cdot \dfrac{1 - \dfrac{1}{2^n}}{1 - \dfrac{1}{2}} \longrightarrow \frac{1}{2} \cdot \dfrac{1}{1 - \dfrac{1}{2}} = 1
\end{align*}$$

khi $n \to \infty$. Như vậy $S_n$ là chuỗi hội tụ.
````

## Tiêu chuẩn Cauchy

Theo định nghĩa, chuỗi số hội tụ khi tồn tại giới hạn hữu hạn. Do đó ta có thể viết theo ngôn ngữ $\delta - \varepsilon$ như đối với dãy số.

````{prf:theorem} Tiêu chuẩn Cauchy
Chuỗi số $\displaystyle{\sum_{i=1}^{\infty} a_i}$ hội tụ nếu với mọi $\varepsilon > 0$, tồn tại $N \in \mathbb{N}$, sao cho với mọi $n \geqslant m \geqslant N$, ta có 

$$\left\lvert \sum_{i=n}^{m} a_i \right\rvert < \varepsilon$$
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Do $\displaystyle{\sum_{i=m}^n a_i = \sum_{i=1}^n a_i - \sum_{i=1}^{m-1} a_i}$ nên chuỗi số hội tụ từ một điểm $m$ nào đó trở đi thì chuỗi hội tụ. Tương tự cho phân kỳ.
```

````{prf:corollary}
Nếu chuỗi số $\displaystyle{\sum_{n=1}^\infty a_i}$ hội tụ thì $\displaystyle{\lim_{n \to \infty} a_n = 1}$.
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Theo tiêu chuẩn Cauchy, với mọi $\varepsilon > 0$, do chuỗi hội tụ nên tồn tại $N \in \mathbb{N}$ sao cho với mọi $n \geqslant m \geqslant N$ ta có $\Bigg\lvert \sum\limits_{i=m}^{n} a_i \Bigg\rvert < \varepsilon$.

Nếu ta chọn $m = n$ thì điều kiện trở thành với mọi $\varepsilon > 0$, tồn tại $N \in \mathbb{N}$ sao cho với mọi $n \geqslant N$ ta có $\lvert a_n \rvert < \varepsilon$. Nói cách khác $\displaystyle{\lim_{n \to \infty} a_n = 0}$ (định nghĩa giới hạn dãy số).
```

Dựa vào tiêu chuẩn Cauchy ta có một số tiêu chuẩn hội tụ hữu dụng như sau.

````{prf:theorem} Tiêu chuẩn thứ nhất về sự hội tụ
Xét hai chuỗi số $\displaystyle{\sum_{n=1}^\infty a_n}$ và $\displaystyle{\sum_{n=1}^\infty b_n}$. Khi điều kiện $0 \leqslant a_n \leqslant b_n$ thỏa mãn, ta có các kết quả sau:

1. Nếu $\sum b_n$ hội tụ thì $\sum a_n$ cũng hội tụ
2. Nếu $\sum a_n$ phân kỳ thì $\sum b_n$ cũng phân kỳ
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Ta thấy rằng nếu $\sum b_n$ hội tụ thì với mọi $\varepsilon > 0$, tồn tại $N \in \mathbb{N}$ sao cho với mọi $n \geqslant m \geqslant N$, $\displaystyle{\Bigg\lvert \sum_{i=m}^n a_i \Bigg\rvert < \varepsilon}$.

Do $0 \leqslant a_i \leqslant b_i$ nên $\displaystyle{\Bigg\lvert \sum_{i=m}^{n} a_i \Bigg\rvert < \Bigg\lvert \sum_{i=m}^{n} b_i \Bigg\rvert < \varepsilon}$. Như vậy chuỗi $\displaystyle{\sum_{n=1}^{\infty} a_n}$ cũng hội tụ.
```

````{prf:theorem} Tiêu chuẩn so sánh
Xét hai chuỗi số dương $\displaystyle{\sum_{n=1}^\infty a_n}$ và $\displaystyle{\sum_{n=1}^\infty b_n}$. Nếu tồn tại giới hạn hữu hạn $\displaystyle{\lim_{n \to \infty} \dfrac{a_n}{b_n} = L}$ thì hai dãy số trên cùng hội tụ hoặc cùng phân kỳ.
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Do dãy số $\dfrac{a_n}{b_n}$ có giới hạn hữu hạn $L$ nên với mọi $\varepsilon > 0$, tồn tại $N \in \mathbb{N}$ sao cho với mọi $n \geqslant N$, ta có $\Big\lvert \dfrac{a_n}{b_n} - L \Big\rvert < \varepsilon$. Tương đương với $\displaystyle{b_n (-\varepsilon + L) < a_n < b_n (\varepsilon + L)}$. Từ tiêu chuẩn thứ nhất về sự hội tụ và bất đẳng thức thứ hai suy ra nếu chuỗi $\sum b_n$ hội tụ thì chuỗi $\sum a_n$ cũng hội tụ.

Tương tự, với bất đẳng thức thứ nhất, nếu $\sum b_n$ phân kỳ thì $\sum a_n$ cũng phân kỳ.
```

````{prf:theorem} Tiêu chuẩn tích phân Cauchy
Xét chuỗi số dương $\displaystyle{\sum_{n=1}^{\infty} a_n}$. Nếu $a_n$ là dãy số có dạng $a_n = f(n)$, ta chuyển qua xét hàm số $f(x)$.

Nếu hàm số $f(x)$ thỏa mãn:

1. $f(x)$ không tăng
2. $\displaystyle{\int\limits_{0}^{\infty} f(x)\,dx}$ hữu hạn

Khi đó chuỗi số $\displaystyle{\sum_{n=1}^{\infty} a_n}$ hội tụ.
````
