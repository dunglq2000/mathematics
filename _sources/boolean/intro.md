# Giới thiệu

```{contents}
:depth: 2
```

## Kí hiệu

| Kí hiệu | Ý nghĩa |
| ------- | ------- |
| $\mathcal{F}_n$ | Tập hợp tất cả hàm boolean $n$ biến |
| $\mathcal{A}_n$ | Tập hợp tất cả hàm boolean affine $n$ biến |
| $\mathcal{L}_n$ | Tập hợp tất cả hàm boolean tuyến tính $n$ biến |
| $\mathrm{wt}(f)$ | Trọng số của hàm boolean $f$ |
| $N_f$ | Nonlinearlity của hàm boolean $f$ |
| $W_f(\bm{a})$ | Hệ số Walsh của hàm $f$ ứng với vector $\bm{a}$ |

## Các tính chất mật mã của hàm boolean

### Bậc đại số cao

Tham số $\deg f$ phải cao. Điều này đặc biệt quan trọng trong các stream cipher sử dụng LFSR.

### Nonlinearlity cao

Kí hiệu nonlinearlity của hàm boolean $f$ là $N_f$. Khái niệm này đã được giải thích ở chương về đại số boolean.

Nonlinearlity cực kì quan trọng trong việc chống phá mã tuyến tính (linear cryptanalysis). Nonlinearlity càng cao, dấu vết tuyến tính càng thấp.

Đối với hàm boolean với số biến là chẵn, nếu có nonlinearlity cực đại (tức bằng $2^{n-1} - 2^{n/2-1}$) được gọi là **hàm bent** (hay **bent function**).

#### Bài tập

1. Chứng minh rằng khoảng cách từ hàm boolean $f$ với $n$ biến tới hàm boolean affine

$$l_{\bm{a}, b}(\bm{x}) = a_1 x_1 \oplus \ldots \oplus a_n x_n \oplus b$$

với $\bm{a} = (a_1, \ldots, a_n) \in \mathbb{F}_2^n$ và $b \in \mathbb{F}_2$ được tính theo công thức:

$$d(f, l_{\bm{a}, 0} (\bm{x})) = 2^{n-1} - \frac{1}{2} W_f(\bm{a}),$$

$$d(f, l_{\bm{a}, 1} (\bm{x})) = 2^{n-1} + \frac{1}{2} W_f (\bm{a})$$

2. Chứng minh rằng nonlinearlity của hàm boolean $f$ bất kì được tính bởi công thức

$$N_f = 2^{n-1} - \frac{1}{2} \max_\bm{y} \lvert W_f (\bm{y}) \rvert$$

3. Chứng minh rằng hàm boolean $f$ là hàm bent khi và chỉ khi $W_f(\bm{y}) = \pm 2^{n/2}$ với mọi vector $\bm{y}$.

### Balanced

Hàm boolean được gọi là **balanced** (hay **cân bằng**, **сбалансированный**) nếu nhận giá trị $0$ và $1$ nhiều như nhau.

**Bài tập:** Xác định số lượng hàm boolean cân bằng có $n$ biến.

````{prf:remark}
Tính cân bằng và nonlinearlity là hai tính chất đối nghịch nhau. Chúng ta rất khó có thể tìm được hàm boolean vừa cân bằng vừa là hàm bent (thậm chí không thể).
````

### $r$-resillient

Đặt $r$ là số nguyên không âm nhỏ hơn $n$. Hàm boolean $f$ với $n$ biến được gọi là **$r$-resillient** (hay **$r$-устойчивой**) nếu với mọi hàm con mà nhận được từ việc cố định $r$ biến thì đều là hàm cân bằng.

Hàm boolean này có độ an toàn cao hơn so với hàm cân bằng, giúp chống lại cách tấn công correlation cryptanalysis.

### Correlation immune

Hàm boolean $f$ với $n$ biến được gọi là **correlation immune of order $r$** (**корреляционно-иммунной порядка $r$**, tạm dịch là *kháng tương quan bậc $r$*) với $1 \leqslant r \leqslant n$ nếu với mọi hàm con $f^{a_1, \ldots, a_r}_{i_1, \ldots, i_r}$ nhận được từ việc cố định $r$ biến thì đều thỏa đẳng thức

$$\mathrm{wt} (f^{a_1, \ldots, a_r}_{i_1, \ldots, i_r}) = \frac{\mathrm{wt}(f)}{2^r}$$

#### Bài tập

1. Chứng minh rằng hàm boolean $f$ là $r$-resillient khi và chỉ khi nó cân bằng và correlation immune bậc $r$.
2. (**Định lí Siegenthaler I**, 1984) Chứng minh rằng nếu hàm boolean $f$ là correlation immune bậc $r$ thì $\deg f + r \leqslant n$.
3. (**Định lí Siegenthaler II**) Chứng minh rằng nếu hàm boolean $f$ là $r$-resillient và $r \leqslant n - 2$ thì $\deg f + r \leqslant n - 1$.

Chứng minh cho các định lí Siegenthaler có thể tìm ở {cite}`Agibalov`.

4. Chứng minh rằng hàm boolean $f$ là correlation immune bậc $r$ khi và chỉ khi $W_f(\bm{y}) = 0$ với mọi vector $\bm{y}$ thỏa $1 \leqslant \mathrm{wt} (\bm{y}) \leqslant r$.

Năm 2007 Д. Г. Фон–Дер–Флаасс tìm được chặn trên cho correlation immune của hàm boolean không cân bằng.

5. (**Định lí Д. Г. Фон–Дер–Флаасс**, {cite}`Flaass`) Gọi $f$ là hàm boolean không rân bằng có correlation immune bậc $r$ khác $0$. Chứng minh rằng $r \leqslant (2n/3) - 1$.
6. Chứng minh rằng với hàm boolean $r$-resillient $f$ sao cho $r \leqslant n-2$ thì ta có bất đẳng thức $N_f \leqslant 2^{n-1} - 2^{r+1}$ {cite}`Cusick`.

### Algebraic immune

Tính chất này được giới thiệu vào năm 2004.

**Algebraic immune** (tạm dịch là *kháng đại số*) của hàm boolean $f$ là số $d$ nhỏ nhất sao cho tồn tại hàm boolean $g$ bậc $d$, không đồng nhất với $0$, thỏa mãn $f g = 0$ hoặc $(f \oplus \bm{1}) g = 0$.

Algebraic immune của hàm $f$ được kí hiệu là $AI(f)$.

Ví dụ algebraic immune hàm $f(\bm{x}) = x_1 x_2 x_3 \oplus x_1$ bằng $1$, vì ta có thể chọn $g(\bm{x}) = x_1 \oplus 1$. Khi đó $f g = (x_1 x_2 x_3 \oplus x_1) (x_1 \oplus 1) = 1$.

#### Bài tập

1. Chứng minh rằng algebraic immune của hàm boolean $f$ bất kì với $n$ biến không vượt quá giá trị $\lceil n/2 \rceil$.
2. Chứng minh một số tính chất cơ bản của algebraic immune:
    - $AI(f) \leqslant \deg f$
    - $AI(f \cdot g) \leqslant AI(f) + AI(g)$
    - $AI(f \oplus g) \leqslant AI(f) + AI(g)$
    - $AI(f) = AI(g)$ nếu $g$ nhận được từ $f$ qua một biến đổi affine trên các biến, nghĩa là $g(\bm{x}) = f(\bm{A} \bm{x} \oplus \bm{b})$ với $\bm{A}$ là ma trận nghịch đảo bậc $n$ và $\bm{b}$ là vector.
3. Xác định giá trị của $AI(f)$ với các hàm boolean sau và tìm hàm $g$ tương ứng:
    - $f(\bm{x}) = x_1 x_2 x_4 \oplus x_1 x_2 \oplus 1$
    - $f(\bm{x}) = 0$
    - $f(\bm{x}) = 1$
    - $f(\bm{x}) = x_1 \cdots x_k$ với $k = 1, 2, \ldots, n$
    - $f(\bm{x}) = x_1 \oplus \ldots \oplus x_n$
    - $f(\bm{x}) = x_1 x_2 \oplus \ldots \oplus x_{n-1} x_n$ (tổng tất cả cặp tích)
    - $f(\bm{x}) = x_1 x_2 x_3 x_4 \oplus x_5 x_6$
4. Cho ví dụ hàm boolean $f$ với giá trị algebraic immune nhỏ nhất, nghĩa là $AI(f) = d$ với $d = 1, 2, \ldots, k$.

### Differentially $\delta$-uniform

Khái niệm này lần đầu được định nghĩa trong {cite}`eurocrypt-1993-2628`.

Hàm boolean vector $F : \mathbb{F}_2^n \to \mathbb{F}_2^n$ gọi là **differentially $\delta$-uniform** nếu với mọi vector $\bm{a}$ khác không và vector $\bm{b}$ bất kì thì phương trình

$$F(\bm{x}) \oplus F(\bm{x} \oplus \bm{a}) = \bm{b}$$

có không quá $\delta$ nghiệm với $\delta$ là số nguyên.

Để ý rằng nếu phương trình có nghiệm là $\bm{x}$ thì cũng có nghiệm $\bm{x} \oplus \bm{a}$. Số $\delta$ càng nhỏ thì phép biến đổi của thuật toán mã hóa càng ít có dấu hiệu tuyến tính, tăng khả năng kháng phá mã vi sai.

Hàm boolean vector được gọi là **hàm APN** nếu differentially uniform với giá trị $\delta$ nhỏ nhất. Trong trường hợp này là $\delta = 2$.

Bài toán khó hiện nay là xây dựng hàm APN là song ánh với số biến $n$ chẵn.

#### Bài tập

Chứng minh hàm $S : \mathbb{F}_2^8 \to \mathbb{F}_2^8$ của S-box trong thuật toán AES là differentially 4-uniform.
