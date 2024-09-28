# Phương trình vi phân

## Phương trình vi phân bậc nhất

Phương trình vi phân bậc nhất có dạng:

$$\begin{equation*}
    P(x, y)\,dx + Q(x, y)\,dy = 0.
\end{equation*}$$

Nghiệm tổng quát có dạng $y = \varphi(x, c)$ khả vi và thỏa mãn điều kiện của phương trình vi phân.

1. Hàm $\varphi(x, c)$ là nghiệm của phương trình vi phân với hằng số $c$.
2. Nếu $y(x_0) = y_0$ thì có thể tìm được $c_0$. Khi đó nghiệm được gọi là **nghiệm riêng** $y = \varphi(x, c_0)$.

````{prf:definition} Phương trình tách biến
**Phương trình tách biến** (hay **разделяющие переменные**) là phương trình có dạng:

$$\begin{equation*}
    P_1(x) \cdot Q_1(y) \, dx + P_2(x) \cdot Q_2(y) \, dy = 0
\end{equation*}$$
````

Để giải phương trình tách biến ta chia hai vế cho $Q_1(y) \cdot P_2(x) \neq 0$ và giải

$$\begin{equation*}
    \int \frac{P_1(x)}{P_2(x)} \, dx + \int \frac{Q_2(y)}{Q_1(y)} \, dy = 0.
\end{equation*}$$

Nếu $Q_1(y) \cdot P_2(x) = 0$ thì ta giải từng hàm riêng $Q_1(y) = 0$ hoặc $P_2(x) = 0$.

````{prf:definition} Hàm thuần nhất bậc $n$
Hàm thuần nhất bậc $n$ với tham số $\lambda$ bất kì ta luôn có $f(\lambda x, \lambda y) = \lambda^n f(x, y)$.
````

Ví dụ, $f(x, y) = x^2 - 2xy$. Với các hàm thuần nhất ta có định nghĩa phương trình vi phân thuần nhất.

````{prf:definition} Phương trình vi phân thuần nhất
Phương trình vi phân $y' = f(x, y)$ được gọi là thuần nhất nếu hàm $f(x, y)$ là hàm thuần nhất bậc $0$. Khi đó $y' = \varphi\left(\dfrac{y}{x}\right)$.
````

Để giải dạng này ta đặt $\dfrac{y}{x} = u$. Như vậy $y = ux$ và $y' = u'x + ux'$.

## Phương trình tuyến tính và phương trình Bernoulli

````{prf:definition} Phương trình vi phân tuyến tính
Phương trình vi phân được gọi là tuyến tính bậc nhất nếu nó có dạng $y' + p(x) \cdot y = g(x)$.
````

Để giải phương trình tuyến tính ta có hai phương pháp là phương pháp Bernoulli và phương pháp Lagrange.

Đối với phương pháp Bernoulli, ta đặt $y = uv$ với $u = u(x)$ và $v = v(x)$ là một hàm được chọn từ lớp các hàm thỏa mãn với hằng số cố định. Khi đó $y' = u'v + uv'$.

Phương trình vi phân khi này có dạng:

$$\begin{align*}
    & y' + p(x) \cdot y = g(x) \\
    \Leftrightarrow & u'v + v'u + p(x) \cdot u v = g(x) \\
    \Leftrightarrow & u'v + u(v' + p(x) \cdot v) = g(x)
\end{align*}$$

Ta chọn $v$ sao cho $v' + p(x) \cdot v = 0$. Điều này tương đương với $\dfrac{dv}{dx} + p(x) \cdot v = 0$ nên $\ln \lvert v \rvert = -\int p(x)\, dx + \ln \lvert C \rvert$. Ở đây $C$ là hằng số.

Để đơn giản, ta chọn $C = 1$ thì $v = e^{-\int p(x) \, dx}$.

Suy ra $u'v = u' e^{-\int p(x)\, dx} = g(x)$ và biến đổi

$$\begin{align*}
    & \frac{du}{dx} \cdot e^{-\int p(x) \, dx} = g(x) \\
    \Leftrightarrow & u = \int g(x) \cdot e^{-\int p(x) \, dx} \, dx + C \\
    \Leftrightarrow & y = uv = \ldots
\end{align*}$$

Đối với phương pháp Lagrange, ta xét phương trình vi phân tuyến tính thuần nhất tương ứng với $y' + p(x) \cdot y = g(x)$ là $y' + p(x) \cdot y = 0$.

Khi đó ta biến đổi $\dfrac{dy}{dx} = -p(x) \cdot y$ và giải được $y = c e^{-\int p(x)\,dx}$ với $c$ là hằng số.

Ta thay $c$ bởi $c(x)$ là hàm theo $x$:

$$\begin{align*}
    & y = c(x) \cdot e^{-\int p(x)\,dx} \\
    \Leftrightarrow & y' = c'(x) \cdot e^{-\int p(x)\,dx} + c(x) \cdot e^{-\int p(x)\,dx} \cdot (-p(x))
\end{align*}$$

và thay vào phương trình vi phân ban đầu:

$$\begin{align*}
    & c'(x) \cdot e^{-\int p(x)\,dx} + \cancel{c(x) \cdot e^{-\int p(x)\,dx} \cdot (-p(x))} + \cancel{c(x) \cdot e^{-\int p(x)\,dx} \cdot p(x)} = g(x) \\
    \Leftrightarrow & c'(x) \cdot e^{-\int p(x)\,dx} = g(x) \\
    \Leftrightarrow & d c(x) = e^{\int p(x)\,dx} \cdot g(x)\,dx
\end{align*}$$

Tới đây ta tìm được $c(x)$ để có $y$.

````{prf:definition} Phương trình Bernoulli
Phương trình Bernoulli là phương trình có dạng:

$$\begin{equation*}
    y' + p(x) \cdot y = g(x) \cdot y^n, \ n \in \mathbb{N}, n \neq 0, n \neq 1.
\end{equation*}$$
````

Khi $n=0$ thì phương trình trở thành phương trình tuyến tính.

Để giải phương trình Bernoulli ta chia hai vế cho $y^n$ thì được:

$$\begin{equation*}
    \frac{y'}{y^n} + \frac{p(x)}{y^{n-1}} = g(x)
\end{equation*}$$

Đặt $\dfrac{1}{y^{n-1}} = z$ thì $z' = \dfrac{dz}{dx} = (1-n) \dfrac{1}{y^n} y'$.

Như vậy $\dfrac{1}{y^n} \cdot y' = \dfrac{z'}{1-n}$ và thay vào phương trình ban đầu ta có

$$\begin{equation*}
    \frac{1}{1-n} z' + p(x) \cdot z = g(x).
\end{equation*}$$

Từ đây ta giải phương trình tuyến tính.

## Phương trình vi phân toàn phần. Nhân tử tích phân

````{prf:definition} Phương trình vi phân toàn phần
Phương trình vi phân được gọi là **toàn phần** (hay **уравнение в полных дифферециалах**) nếu vế trái có vi phân toàn phần là hàm $u(x, y)$, nghĩa là:

$$\begin{equation*}
    P(x, y) \, dx + Q(x, y) \, dy = d u(x, y).
\end{equation*}$$
````

````{prf:theorem}
Điều kiện cần và đủ để biểu thức

$$\begin{equation*}
    \Delta = P(x, y) \,dx + Q(x, y)\,dy,
\end{equation*}$$

với $P(x,y)$ và $Q(x,y)$ và đạo hàm riêng $\dfrac{\partial P}{\partial y}$ và $\dfrac{\partial Q}{\partial x}$ liên tục trên tập $D$ nào đó, là phương trình vi phân toàn phần:

$$\begin{equation*}
    \frac{\partial P}{\partial y} = \frac{\partial Q}{\partial x}.
\end{equation*}$$
````

```{admonition} **Chứng minh**
:class: danger

Để chứng minh điều kiện cần, đặt $\Delta$ là biểu thức có vi phân toàn phần, nghĩa là

$$\begin{align*}
    & P(x, y) \, dx + Q(x, y) \, dy = d u(x, y) \\
    \Leftrightarrow & d u(x, y) = \frac{\partial u}{\partial x} \, dx + \frac{\partial u}{\partial y} \, dy,
\end{align*}$$

với $P(x, y) = \dfrac{\partial u}{\partial x}$ và $Q(x, y) = \dfrac{\partial u}{\partial y}$. 

Suy ra $\dfrac{\partial P}{\partial y} = \dfrac{\partial^2 u}{\partial x \partial y}$ và $\dfrac{\partial Q}{\partial x} = \dfrac{\partial^2 u}{\partial y \partial x}$.

Khi đó $\dfrac{\partial P}{\partial y} = \dfrac{\partial Q}{\partial x}$ và ta có điều phải chứng minh.

Để chứng minh điều kiện đủ, trên tập $D$ ta có $\dfrac{\partial P}{\partial y} = \dfrac{\partial Q}{\partial x}$.

Lúc này ta chứng minh tồn tại hàm $u(x, y)$ trên $D$ mà $d u(x, y) = P(x, y)\,dx + Q(x, y)\,dy$.

Giả sử ngược lại, $\dfrac{\partial u}{\partial x} = P(x, y)$ và $\dfrac{\partial u}{\partial y} = Q(x, y)$.

Ở đây, ta cố định $y$ và lấy tích phân theo $x$ thì được:

$$\begin{equation*}
    u(x, y) = \int P(x, y)\,dx + \varphi(y),
\end{equation*}$$

với $c = \varphi(y)$ là hằng số (do $y$ cố định nên $\varphi(y)$ cũng cố định). Suy ra ta có:

$$\begin{align*}
    \frac{\partial u}{\partial y} = \left( \int P(x, y)\,dx\right)'_y + \varphi'(y) \\
    \Leftrightarrow Q(x, y) = \left( \int P(x, y)\,dx\right)'_y + \varphi'(y) \\
    \Leftrightarrow \varphi'(y) = Q(x, y) - \left( \int P(x, y)\,dx\right)'_y
\end{align*}$$

Vế phải khi đạo hàm theo $x$ là:

$$\begin{align*}
    & \frac{\partial}{\partial x}\left( Q(x, y) - \frac{\partial}{\partial y} \left(\int P(x, y)\,dx\right) \right) \\
    = & \frac{\partial Q}{\partial x} - \frac{\partial}{\partial x}\left( \frac{\partial}{\partial y} \left( \int P(x, y)\,dx \right) \right) \\
    = & \frac{\partial Q}{\partial x} - \frac{\partial}{\partial y}\left( \frac{\partial}{\partial x} \left( \int P(x, y)\,dx \right) \right) \\
    = & \frac{\partial Q}{\partial x} - \frac{\partial}{\partial y} (P) = 0,
\end{align*}$$

từ đây suy ra:

$$\begin{equation*}
    \varphi(y) = \int \left( Q(x, y) - \frac{\partial}{\partial y} \left(\int P(x, y)\,dx\right) \right)\,dy + c,
\end{equation*}$$

với $c$ là hằng số.

Khi điều kiện $\dfrac{\partial P}{\partial y} = \dfrac{\partial Q}{\partial x}$ không thỏa mãn, ta nhân thêm hàm $t(x, y)$ để thỏa điều kiện:

$$\begin{equation*}
    \frac{\partial}{\partial y}(t(x, y) \cdot P(x, y)) = \frac{\partial}{\partial x} (t(x, y) \cdot Q(x, y)).
\end{equation*}$$

Hàm $t(x, y)$ khi đó được gọi là **nhân tử tích phân** (hay **интегрирующий множитель**). Lúc này phương trình biến đổi thành:

$$\begin{align*}
    \frac{\partial t}{\partial y} \cdot P + \frac{\partial P}{\partial y} \cdot t = \frac{\partial t}{\partial x} \cdot Q + \frac{\partial Q}{\partial x} \cdot t \\
    \Leftrightarrow \frac{\partial t}{\partial y} \cdot P - \frac{\partial t}{\partial x} \cdot Q = t \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right).
\end{align*}$$

Lúc này ta chỉ cần tìm hàm $t$ chỉ phụ thuộc $x$ hoặc $y$. Ví dụ với $t = t(x)$ ta có thể biến đổi:

$$\begin{align*}
    & -\frac{dt}{dx} Q = t \left(\frac{\partial Q}{\partial x} - \frac{\partial P}{\partial y}\right) \\
    \Leftrightarrow & \frac{dt}{t} = \frac{\partial P / \partial y - \partial Q / \partial x}{Q} \, dx \\
    \Leftrightarrow & t(x) = \exp\left(\int \frac{\partial P / \partial y - \partial Q / \partial x}{Q} \, dx \right)
\end{align*}$$

Tương tự, $\displaystyle t(y) = \exp \left( \int \frac{\partial Q / \partial x - \partial P / \partial y}{P} \, dy \right)$.
```

## Phương trình Lagrange và Clairaut

````{prf:definition} Phương trình Lagrange
Phương trình Lagrange (уравнение Лагранжа) là phương trình có dạng:

$$\begin{equation*}
    y = x \varphi(y') + \psi(y'),
\end{equation*}$$

với $\varphi$ và $\psi$ là hai hàm số với $y' = \dfrac{dy}{dx}$.
````

Để giải phương trình Lagrange ta đặt $p = y'$. Khi đó $y = x \varphi(p) + \psi(p)$. Lấy vi phân hai vế ta có:

$$\begin{align*}
    \frac{dy}{dx} & = \varphi(p) + x \varphi'(p) p'+ \psi'(p) p' \\
    & = \varphi(p) + x \varphi'(p) \frac{dp}{dx} + \psi'(p) \frac{dp}{dx}.
\end{align*}$$

Thay vào điều kiện ban đầu ta được:

$$\begin{equation*}
    (p - \varphi(p)) \frac{dx}{dp} - x \varphi'(x) = \psi'(p).
\end{equation*}$$

Đây là phương trình vi phân tuyến tính theo $x = x(p)$.

Giải phương trình tìm được $x = \lambda(p, c)$ với $c$ là hằng số, thay lại điều kiện $p = y'$ tìm được $y = \gamma(x, c)$.

Chú ý rằng khi thay vào điều kiện ban đầu ta chia cho $dp$ nên trước đó phải xét trường hợp $dp = 0$, nói cách khác $p = p_0$ là hằng số và $p - \varphi(p) = 0$.

Nghiệm $y = x \varphi(p_0) + \psi(p_0)$ gọi là **nghiệm đặc trưng** (hay **особое решение**).

````{prf:definition} Phương trình Clairaut
Phương trình Clairaut (уравнение Клеро) có dạng:

$$\begin{equation*}
    y = x y' + \psi(y')
\end{equation*}$$
````

Đây là phương trình Lagrange khi $\varphi(y') = y'$.

Để giải phương trình này, đặt $y' = p$ thì $y = xp + \psi(p)$. Khi đó:

$$\begin{align*}
    & \frac{dy}{dx} = p + xp' + \psi'(p) p' \\
    \Leftrightarrow & p = p + x \frac{dp}{dx} + \psi'(p) \frac{dp}{dx} \\
    \Leftrightarrow & (x + \psi'(p)) \frac{dp}{dx} = 0
\end{align*}$$

Nếu $\dfrac{dp}{dx} = 0$ thì $p = c$ là hằng số. Nghiệm tổng quát là $y = cx + \psi(c)$.

Nếu $x + \psi'(p) = 0$ thì $x = -\psi'(p)$. Suy ra $y = xp + \psi(p)$  là nghiệm đặc trưng và không có dạng tổng quát.