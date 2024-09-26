## Internet Olympiad 2024

### Vòng 2

#### Bài 2

##### Đề bài

Cho hai số tự nhiên $x, y$ sao cho

$$A = \dfrac{2y}{x(y-x)}, B = \dfrac{(y-x)(y+1)}{2y^2} \in \mathbb{Z}.$$

Tìm $x, y$.

##### Lời giải

Do $A, B \in \mathbb{Z}$ nên

$$A \cdot B = \dfrac{2y}{x(y-x)} \cdot \dfrac{(y-x)(y+1)}{2y^2} = \dfrac{y+1}{xy} \in \mathbb{Z}$$

Suy ra tồn tại $k \in \mathbb{Z}$ sao cho $y + 1 = kxy$, tương đương với $y(kx - 1) = 1$. Điều này chỉ xảy ra khi $y = 1, x = 2$ (có một nghiệm khác là $y = 1, x = 1$ nhưng sẽ không thỏa mẫu số của $A$).

#### Bài 8

##### Đề bài

Cho $x, y$ là các số thực thỏa $x^2 + y^2 + xy = x + y$. Tìm giá trị lớn nhất của $x^2 + y^2$.

##### Lời giải

Thầy mình bảo đây là dạng bậc hai nên có thể biến đổi để thành phương trình ellipse. Ở đây mình giải theo cách của mình.

Ta có

$$\begin{align*}
    x^2 + y^2 + xy = & x + y \\
    2x^2 + 2y^2 + 2xy = & 2x + 2y \\
    x^2 + y^2 = & -(x+y)^2 + 2(x+y) = -t^2 + 2t = f(t)
\end{align*}$$

Ta có $f'(t) = -2t + 2$, $f'(t) = 0 \Leftrightarrow t = 1$. 

Do đó $f(t)_{\max} = f(1) = 1$.

#### Bài 9

##### Đề bài

Xét đa thức $P(x) = x^4 - 4x^2 - x + 1$. Tính $\displaystyle{\sum_{i=1}^4 \dfrac{2x_i + 1}{(x_i^2 - 1)^2}}$ với $x_i$ là các nghiệm của $P(x)$.

##### Lời giải

Ta biến đổi

$$P(x) = x^4 - 4x^2 - x + 1 = (x^2-1)^2 - x(2x+1).$$

Do $x_i$ là nghiệm nên $P(x_i) = 0$, tương đương với $\dfrac{1}{x_i} = \dfrac{2x_i+1}{(x_i^2-1)^2}$.

Tổng trên tương đương với $\sum \dfrac{1}{x_i}$. Dùng Viete có thể tính ra.

#### Bài 10

##### Đề bài

Cho hàm số

$$\begin{equation*}
    f(x) = \frac{4x - 3}{(x+2)(x+2^2) \ldots (x+2^{2023})}
\end{equation*}$$

Gọi $M$ là đạo hàm của $f(x)$ tại $x_0 = 0$. Tính giá trị $2^{1013 \cdot 2023} \cdot M - 7 \cdot 2^{2023}$.

##### Lời giải

Đặt $f(x) = \dfrac{4x-3}{g(x)}$ thì 

$$f'(x) = \dfrac{4 g(x) - (4x - 3) g'(x)}{g^2(x)}.$$

Do

$$g(x) = \prod_{i=1}^{2023} (x + 2^i),$$

ta lấy log hai vế thì được

$$\ln g = \sum_{i=1}^{2023} \ln (x + 2^i)$$

Suy ra

$$\dfrac{g'}{g} = \sum_{i=1}^{2023} \dfrac{1}{x+2^i}$$

nên suy ra

$$g'(0) = g(0) \cdot \sum_{i=1}^{2023} \dfrac{1}{2^i}$$

Như vậy $f'(0) = \dfrac{4 - 3 \sum_{i=1}^{2023} \dfrac{1}{2^i}}{\prod_{i=1}^{2023} 2^i} = M$.
