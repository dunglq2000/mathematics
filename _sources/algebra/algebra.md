# Đại cương về tập hợp

```{contents}
:depth: 2
```

Tập hợp là khái niệm nền tảng, có mặt trong hầu khắp các ngả rẽ của toán học. Mình có dịp đọc quyển *Toán học qua các câu chuyện về tập hợp* của Tủ sách Sputnik {cite}`Sputnik008`, dịch từ quyển *Рассказы о множествах* của Виленкин Н.Я. {cite}`Vilenkin19` và thấy những câu chuyện rất thú vị. Nếu hứng thú các bạn có thể tìm đọc.

## Tập hợp

### Mở đầu về tập hợp

Một **tập hợp** (**set**) bao gồm các phần tử khác nhau. Tập hợp là khái niệm cơ sở cho nhiều vấn đề của toán học. Tuy nhiên chúng ta lại không có một định nghĩa chặt chẽ về tập hợp mà chỉ có thể biểu diễn nó. Để biểu diễn tập hợp ta có hai cách.

1. Liệt kê. Ví dụ $A = \{ 1, 2, 3, 4 \}$, $B = \{ a, b , c \}$
2. Sử dụng tính chất đặc trưng. Ví dụ $A = \{ a \in \mathbb{N}^* : a < 5 \}$.

Ở đây hai cách biểu diễn tập hợp $A$ là giống nhau.

````{prf:definition} Tập hợp rỗng
Tập hợp rỗng không chứa phần tử nào, ký hiệu là $\emptyset$.
````

````{prf:definition} Tập hợp con
Xét tập hợp $A$. Tập hợp $B$ được gọi là **tập hợp con** của tập $A$ nếu mọi phần tử của $B$ đều nằm trong $A$. Nói cách khác với mọi $b \in B$ thì $b \in A$. Ta ký hiệu $B \subset A$.
````

````{prf:remark}
Tập hợp rỗng là con của mọi tập hợp.
````

Dễ thấy rằng mọi tập hợp là tập hợp con của chính nó. Do đó tập con này được gọi là tập con tầm thường (trivial subset). Để ký hiệu một tập con có thể bằng tập chứa nó ta viết $B \subseteq A$. Trong trường hợp $B$ là tập con của $A$ nhưng không bằng $A$ ta có thể viết $B \subsetneq A$.

### Toán tử trên tập hợp

Chúng ta xem xét ba toán tử cơ bản trên tập hợp là **giao**, **hợp** và **hiệu** của hai tập hợp. Để biểu diễn các toán tử này ta có thể dùng biểu đồ Venn.

````{prf:definition} Giao của hai tập hợp
Giao của hai tập hợp $A$ và $B$ là tập hợp các phần tử thuộc cả $A$ và $B$.

$$\begin{equation}
    A \cap B = \{ x : x \in A \text{ và } x \in B \}
\end{equation}$$
````

```{figure} ../figures/set/venn_diagram-1.jpg
:name: set1

Phép giao hai tập hợp
```

{numref}`set1` là biểu đồ Venn tương ứng của phép giao hai tập hợp. Khi giao của hai tập hợp $A$ và $B$ là rỗng thì ta nói hai tập rời nhau. Ký hiệu $A \cap B = \emptyset$.

````{prf:definition} Hợp của hai tập hợp
Hợp của hai tập hợp $A$ và $B$ là tập hợp các phần tử thuộc $A$ hoặc $B$.

$$\begin{equation}
    A \cup B = \{ x : x \in A \text{ hoặc } x \in B \}
\end{equation}$$
````

{numref}`set2` là biểu đồ Venn tương ứng của phép hợp hai tập hợp.

```{figure} ../figures/set/venn_diagram-2.jpg
:name: set2

Phép hợp hai tập hợp
```

````{prf:definition} Hiệu của hai tập hợp
Hiệu (hay phần bù) của tập hợp $A$ đối với tập hợp $B$ là tập hợp các phần tử thuộc $A$ nhưng không thuộc $B$.

$$\begin{equation}
    A \backslash B = \{ x : x \in A \text{ và } x \not\in B \}
\end{equation}$$
````

{numref}`set3` là biểu đồ Venn tương ứng của hiệu hai tập hợp.

```{figure} ../figures/set/venn_diagram-3.jpg
:name: set3

Phép hiệu hai tập hợp
```

## Lực lượng của tập hợp

Để chỉ số lượng phần tử của một tập hợp ta dùng khái niệm lực lượng của tập hợp.

Ký hiệu lực lượng của tập hợp $A$ là $\lvert A \rvert$ hoặc $\# A$.

Khi một tập hợp có vô số phần tử, ta gọi đó là tập vô hạn. Ngược lại ta gọi là tập hữu hạn.

````{prf:example}
Các tập hợp số thông dụng $\mathbb{N}$, $\mathbb{Z}$, $\mathbb{Q}$, $\mathbb{R}$ là các tập vô hạn.

Tập hợp $A = \{ 1, 2, 3, 4, 5 \}$ là tập hữu hạn có 5 phần tử. Ký hiệu $\lvert A \rvert = 5$.
````

Từ biểu đồ Venn chúng ta cũng có thể tìm được công thức tính lực lượng của tập $A \cup B$.

```{figure} ../figures/set/venn_diagram-4.jpg
:name: set4

Nguyên lý bù trừ cho hai tập hợp
```

Dựa vào hình ta có thể suy ra công thức sau:

$$\begin{equation*}
    \lvert A \cup B \rvert = \lvert A \rvert + \lvert B \rvert - \lvert A \cap B \rvert
\end{equation*}$$

## Ánh xạ

### Ánh xạ

Cho hai tập hợp $X$ và $Y$. Ánh xạ $f$ biến một phần tử $x \in X$ thành một và chỉ một phần tử $y \in Y$.

Ta ký hiệu

$$f: X \to Y, \; f(x) = y$$

Khi đó, $X$ được gọi là **tập nguồn** (hay **domain**) và $Y$ là **tập đích** (hay **image**).

Ánh xạ có ba loại:

1. **Đơn ánh** (hay **Injection**): Hai phần tử khác nhau của tập nguồn cho hai ảnh khác nhau. Tức là với mọi $x_1, x_2 \in X$ mà $x_1 \neq x_2$, thì $f(x_1) \neq f(x_2)$
2. **Toàn ánh** (hay **Surjection**): Mọi phần tử $y \in Y$ đều có ít nhất một phần tử $x \in X$ mà $f(x) = y$. Nói cách khác với mỗi phần tử trong $Y$ ta đều tìm được phần tử thuộc $X$ biến thành nó
3. **Song ánh** (hay **Bijection**): Nếu ánh xạ đó vừa là đơn ánh, vừa là toàn ánh

Dựa vào định nghĩa và hình vẽ, ta có thể rút ra kết luận như sau

1. Đối với đơn ánh, do mọi phần tử của $X$ đều có ảnh ở $Y$, tuy nhiên có thể có phần tử ở $Y$ không do phần tử nào của $X$ biến thành (trong hình là 5). Do đó $\lvert X \rvert \leqslant \lvert Y \rvert$.
2. Đối với toàn ánh, mọi phần tử của $Y$ đều có nguồn gốc xuất xứ, tuy nhiên có thể có phần tử của $X$ không biến thành $y$ nào của $Y$ (trong hình là $e$). Do đó $\lvert X \rvert \geqslant \lvert Y \rvert$.
3. Đối với song ánh, do là kết hợp giữa đơn ánh và toàn ánh, khi đó dấu đẳng thức xảy ra, $\lvert X \rvert = \lvert Y \rvert$.

```{figure} ../figures/maps-1.jpg

Đơn ánh
```

```{figure} ../figures/maps-2.jpg

Toàn ánh
```

```{figure} ../figures/maps-3.jpg

Song ánh
```

````{prf:definition} Ánh xạ ngược
Ánh xạ ngược của ánh xạ của $\phi: X \to Y$, thường được ký hiệu là $\phi^{-1}$ là ánh xạ biến phần tử từ tập $Y$ vào tập $X$, tức là $\phi^{-1}: Y \to X$, $y \to x$.
````

Tuy nhiên cần lưu ý khi này tập xác định đã trở thành $Y$ nên phải giới hạn lại các phần tử làm giá trị $\phi^{-1}(y)$ xác định.

````{prf:example}
Xét hàm số $f: \mathbb{R} \to \mathbb{R}$, $x \to y=f(x)=x^2$.

Lúc này, $y \geqslant 0$ với mọi $x$ và mình có thể biểu diễn hàm ngược là $x=\sqrt{y}$. Lúc này ánh xạ ngược sẽ trở thành $f^{-1}: \mathbb{R}^{+} \to \mathbb{R}^{+}$
````

````{prf:definition} Ánh xạ hợp
Xét hai ánh xạ $f: X \to Y$, $f(x) = y$ và $g: Y \to Z$, $z = g(y)$. Ánh xạ hợp của $g$ và $f$ được ký hiệu là $g \circ f: X \to Z$, $z = g(y) = g(f(x))$.
````

````{prf:definition} Tích Descartes
Tích Descartes của hai tập hợp $A = \{ a_1, a_2, \cdots, a_n \}$ và $B = \{ b_1, b_2, \cdots, b_m \}$ là tập hợp $S A \times B = \{ (a_i, b_j) : a_i \in A, b_j \in B\}$.
````

````{prf:example}
Với $A = \{1, 2, 3\}$ và $B = \{4, 5\}$ thì tích Descartes là 

$$S = A \times B = \{(1, 4), (1, 5), (2, 4), (2, 5), (3, 4), (3, 5)\}.$$
````

Với nhiều tập hợp thì định nghĩa tương tự.

````{prf:example}
Xét ba tập nguồn $X$, $Y$, $Z$, và tập đích là $T$, ánh xạ $\phi : X \times Y \times Z \to T$, với $\phi(x, y, z) \to t$ là ánh xạ ba biến, tập nguồn của ánh xạ khi này là tích Descartes $X \times Y \times Z$.
````

### Hàm số

Khi hai tập nguồn và đích của ánh xạ là hai tập hợp số, ta có hàm số.

````{prf:example}
Hàm số $f: \mathbb{R} \rightarrow \mathbb{R}$ với $y = f(x) = x^3 + x + 1$. Ở đây $X \equiv \mathbb{R}$ và $Y \equiv \mathbb{R}$.
````

Lưu ý rằng tập nguồn và đích không nhất thiết là tập hợp số cơ bản ($\mathbb{Q}, \mathbb{R}$) mà cũng có thể là tích Descartes của chúng.

````{prf:example}
Hàm số $f: \mathbb{R} \times \mathbb{R} \rightarrow \mathbb{R}$ với $z = f(x, y) = x + y + xy$. Ở đây $X \equiv \mathbb{R}$, $Y \equiv \mathbb{R}$ và $Z \equiv \mathbb{R}$.
````

Chúng ta còn một cách gọi khác cho đơn ánh, toàn ánh, song ánh trong tiếng Anh.

````{prf:example}
Hàm số $f: \mathbb{R} \rightarrow \mathbb{R}$ cho bởi $y = f(x) = x^3$ là song ánh.
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Ta thấy nếu $f(x_1) = f(x_2)$, tương đương $x_1^3 = x_2^3$ nên $x_1 = x_2$. Do đó $f$ là đơn ánh.

Với mọi $y = x^3 \in \mathbb{R}$, do căn bậc ba luôn tồn tại nên ta có $x = \sqrt[3]{y}$. Nghĩa là luôn tồn tại $x$ để $f(x) = y$ với mọi $y \in \mathbb{R}$. Do đó $f$ là toàn ánh.

Kết luận $f$ là song ánh.
```

### Đồng biến và nghịch biến

````{prf:definition} Hàm số đồng biến
Xét hàm số $f(x)$ xác định trên khoảng $(a, b)$. Ta nói $f(x)$ **đồng biến** (**tăng**) trên $(a, b)$ nếu với mọi $x_1, x_2 \in (a, b)$ mà $x_1 < x_2$ ta có $f(x_1) < f(x_2)$.
````

Tương tự $f(x)$ **nghịch biến** (**giảm**) trên $(a, b)$ nếu với mọi $x_1, x_2 \in (a, b)$ mà $x_1 < x_2$ ta có $f(x_1) > f(x_2)$.

Lưu ý ở các so sánh trên dấu bằng có thể xảy ra. Khi đó hàm số được gọi là tăng **không nghiêm ngặt** (hoặc giảm **không nghiêm ngặt**).

Nếu hàm số đồng biến (hoặc nghịch biến) trên khoảng xác định nào đó thì ta nói hàm số đơn điệu trên khoảng đó.

Đồ thị của hàm số khi đồng biến sẽ đi lên (theo chiều từ trái sang phải), và đi xuống nếu nghịch biến.

````{prf:example}
Khảo sát sự biến thiên của hàm số $f(x) = x^2 + 3$.

Để khảo sát sự biến thiên, một cách làm đơn giản theo định nghĩa là ta xét $x_1 < x_2$ và so sánh $f(x_1)$ với $f(x_2)$.

Ta có $f(x_1) - f(x_2) = x_1^2 + 3 - x_2^2 - 3 = (x_1 - x_2)(x_1 + x_2)$

Do $x_1 < x_2$, nên với $x_1, x_2 > 0$ thì $x_1 + x_2 > 0$ và $x_1 - x_2 < 0$. Suy ra $f(x_1) - f(x_2) < 0$ và từ đó $f(x_1) < f(x_2)$. Như vậy $f(x)$ đồng biến trên $(0, +\infty)$.

Tương tự, khi $x_1, x_2 < 0$ thì $x_1 + x_2 < 0$. Khi đó $f(x_1) > f(x_2)$ nên $f(x)$ nghịch biến trên $(-\infty, 0)$.
````

Để thể hiện sự biến thiên của hàm số ta sử dụng bảng biến thiên.

Đối với hàm số $y = x^2 + 3$ ở trên bảng biến thiên có dạng:

```{figure} ../figures/table_of_variation-1.jpg

Bảng biến thiên hàm số $y=x^2 + 3$
```

Ta đã chứng minh được hàm số nghịch biến trên $(-\infty, 0)$ và đồng biến trên $(0, +\infty)$, giá trị $f(0) = 3$ nên bảng biến thiên thể hiện sự tăng giảm trên các khoảng. Dựa vào bảng biến thiên ta có thể hình dung ra dạng của đồ thị hàm số.

### Đồ thị hàm số

Để biểu diễn sự phụ thuộc của biến $y$ theo biến $x$, hay nói cách khác là biểu diễn hàm số $y=f(x)$ ta có thể dùng đồ thị.

Đồ thị được vẽ trên hệ tọa độ Descartes $Oxy$. Bảng biến thiên cho ta thấy tính đơn điệu trên các khoảng xác định, và đồ thị sẽ cho ta thấy rõ hơn độ "cong" của những đường cong.

````{prf:example}
Với hàm số $y = x^2 + 3$ ở trên. Đồ thị hàm số có dạng như {numref}`func1`.

Với hàm số $y = \dfrac{1}{x}$. Ta thấy rằng hàm số không xác định tại $x=0$. Khảo sát sự biến thiên như bên trên ta thấy hàm số nghịch biến ở hai khoảng xác định là $(-\infty, 0)$ và $(0, +\infty)$. Đồ thị hàm số có dạng như {numref}`func2`.
````

```{figure} ../figures/table_of_variation-2.jpg
:name: func1

Đồ thị hàm số $y=x^2 + 3$
```

```{figure} ../figures/table_of_variation-3.jpg
:name: func2

Đồ thị hàm số $y = \dfrac{1}{x}$
```

Từ đồ thị của 2 hàm số trên ta thấy rằng mặc dù cùng là nghịch biến trên $(-\infty, 0)$ nhưng nghịch biến của $y=x^2+3$ nhìn "nhẹ nhàng" hơn. Trong khi  đồ thị $y = \dfrac{1}{x}$ thì ban đầu "nhẹ nhàng", sau thì như "rơi tự do".

## Một số loại hàm số

Một số hàm số có tính chất đặc biệt giúp chúng ta tiết kiệm công sức trong chứng minh, tính toán.

### Hàm chẵn và hàm lẻ

Xét hàm số $y=f(x)$ xác định trên miền $D$ có tính đối xứng, nghĩa là với mỗi phần tử dương $x \in D$ thì có phần tử âm $-x \in D$ hoặc ngược lại. Khi đó

````{prf:definition} Hàm số chẵn
Hàm số $y=f(x)$ được gọi là **hàm số chẵn** nếu với mọi $x \in D$ ta có $f(-x) = f(x)$.
````

Ví dụ như hàm số $y = x^2 + 3$ ở trên là một hàm chẵn vì với mọi $x \in \mathbb{R}$, $f(x) = x^2 + 3 = (-x)^2 + 3 = f(-x)$. Dễ thấy rằng hàm chẵn đối xứng qua trục tung. Dựa vào tính chất này, trong lúc khảo sát hoặc tính toán đôi khi ta chỉ cần quan tâm một bên trục tung, bên kia tương tự.

````{prf:definition} Hàm số lẻ
Hàm số $y=f(x)$ được gọi là **hàm số lẻ** nếu với mọi $x \in D$ ta có $f(-x) = -f(x)$.
````

Ví dụ như hàm số $y = \dfrac{1}{x}$ ở trên là một hàm lẻ vì với mọi $x \in (-\infty, 0) \cup (0, +\infty)$, $f(-x) = \dfrac{1}{-x} = -\dfrac{1}{x} = -f(x)$. Dễ thấy rằng hàm lẻ đối xứng qua gốc tọa độ $O$.

### Hàm cộng tính

Xét hàm số $y=f(x)$ xác định trên miền $D$. 

````{prf:definition} Hàm cộng tính
Hàm số $y = f(x)$ được gọi là **cộng tính** nếu với mọi $x, y \in D$ mà $x + y \in D$, ta có $f(x+y) = f(x) + f(y)$.
````

````{prf:example}
Hàm số $y = 2x$ trên $\mathbb{R}$ là hàm cộng tính vì với mọi $x, y \in \mathbb{R}$, ta có $f(x+y) = 2(x+y) = 2x + 2y = f(x) + f(y)$.
````

### Hàm nhân tính

Tương tự hàm cộng tính, ta định nghĩa hàm nhân tính.

````{prf:definition} Hàm nhân tính
Hàm số $y = f(x)$ được gọi là **nhân tính** nếu với mọi $x, y \in D$ ta có $f(xy) = f(x) \cdot f(y)$.
````

Hàm nhân tính quan trọng được sử dụng trong số học là hàm $\varphi$ Euler về số lượng các số nguyên tố cùng nhau với số nguyên dương $n$. Nếu một hàm số học là nhân tính thì chúng ta chỉ cần quan tâm giá trị của hàm số đó tại các số nguyên tố là đủ.

### Hàm tuần hoàn

Xét hàm số $y=f(x)$ xác định trên miền $D$.

````{prf:definition} Hàm tuần hoàn
Hàm số $y=f(x)$ được gọi là **tuần hoàn** nếu tồn tại số $T$ sao cho $f(x+T) = f(x)$ với mọi $x \in D$.
````

Nói cách khác, hàm số sẽ lặp lại sau một đoạn nhất định.

Số $T$ nhỏ nhất thỏa mãn $f(x+T) = f(x)$ được gọi là **chu kỳ** của hàm tuần hoàn. Vì sao lại là nhỏ nhất?

Ta thấy rằng, nếu $f(x+T) = f(x)$ với mọi $x \in D$, ta thay $x$ bởi $x + T$ thì thu được $f(x + T + T) = f(x+T)$, hay $f(x+2T) = f(x+T)$. Suy ra $f(x+2T) = f(x+T) = f(x)$. Như vậy thì sau $2T$ hàm số cũng lặp lại đúng trạng thái đó. Tương tự cho $3T$, $4T$, .... Do đó số $T$ nhỏ nhất thỏa mãn đẳng thức $f(x+T) = f(x)$ sẽ là chu kỳ.

````{prf:example}
Hàm số $y = \sin(x)$ là hàm tuần hoàn với chu kỳ $T = 2\pi$. Do đó chúng ta chỉ cần khảo sát hàm số trong khoảng $(-\pi, \pi)$ thôi là đủ.
````

## Phép quy nạp toán học

Giả sử ta muốn chứng minh một mệnh đề $P$ đúng với mọi $n \geqslant 1$. Phép quy nạp toán học hoạt động theo ba bước như sau:

1. Chứng minh mệnh đề $P$ đúng với $n=1$ (bước cơ sở)
2. Giả sử mệnh đề $P$ đúng với $n = k \geqslant 1$. Đây gọi là giả thiết quy nạp
3. Chứng minh mệnh đề $P$ đúng với $n = k+1$ từ giả thiết quy nạp bên trên

Như vậy phép quy nạp toán học hoạt động theo bậc thang. Từ giả thiết quy nạp mệnh đề $P$ đúng với $n = 1$, theo chứng minh ở bước (3) thì nó cũng đúng ở bước $n = 1+1 = 2$. Do $P$ đúng với $n=2$ nên cũng đúng ở $n=3$. Cứ tiếp tục như vậy $P$ sẽ đúng với mọi $n \geqslant 1$. Đây là sự hiệu quả đáng kinh ngạc của phép quy nạp toán học.

````{prf:example}
Chứng minh công thức tổng quát cho tổng $1 + 2 + \ldots + n$ là $\dfrac{n(n+1)}{2}$.

Với $n = 1$ thì $1 = \dfrac{1 (1 + 1)}{2}$. Như vậy công thức đúng cho $n = 1$. Đây là bước cơ sở.

Giả sử mệnh đề đúng với $n = k \geqslant 1$. Nghĩa là $1 + 2 + \ldots + k = \dfrac{k(k+1)}{2}$. Đây là giả thiết quy nạp.

Bây giờ ta cần chứng minh mệnh đề đúng với $n = k+1$. Nghĩa là cần chứng minh 

$$1 + 2 + \ldots + k + (k+1) = \dfrac{(k+1)(k+2)}{2}$$

Từ giả thiết quy nạp ta suy ra

$$\begin{align*}
    1 + 2 + \ldots + k + (k+1) = & \dfrac{k(k+1)}{2} + (k+1) \\ = & \dfrac{k(k+1) + 2(k+1)}{2} \\ = & \dfrac{(k+1)(k+2)}{2}
\end{align*}$$

Vậy là ta đã có điều cần chứng minh, và công thức đã được chứng minh đúng với mọi $n \geqslant 1$.
````

````{prf:remark}
Tùy thuộc bài toán, bước cơ sở có thể không phải $1$ mà là một số nguyên dương nào đó khác.
````

## Bảng thuật ngữ

| Tiếng Việt | Tiếng Anh | Tiếng Anh kiểu 2 (?) | Tiếng Nga |
| ---------- | --------- | -------------------- | --------- |
| tập hợp | set | | множество |
| tập hợp rỗng | empty set | | пустое множество |
| lực lượng (của tập hợp) | cardinality | | мощность |
| phép giao tập hợp | intersection of sets| | пересечение множеств |
| phép hợp tập hợp | union of sets | | объединение множеств |
| phép hiệu hai tập hợp | set difference | | разность двух множеств |
| ánh xạ | map | | отображение |
| đơn ánh | injection | one-to-one map | инъекция |
| toàn ánh | surjection | onto map | сюръекция |
| song ánh | bijection | one-to-one and onto map | биекция |
| hàm số | function | | функция |
| hàm đơn điệu | monotonic function | | монотонная функция |
| (hàm số) đồng biến | increasing | | возрастающая |
| (hàm số) tăng nghiêm ngặt | strictly increasing | | строго возрастающая |
| (hàm số) nghịch biến | decresing | | убывающая |
| (hàm số) giảm nghiêm ngặt | strictly increasing | | строго убывающая |
| hàm số chẵn | even function | | четная функция |
| hàm số lẻ | odd function | | нечетная функция |
| hàm cộng tính | additive function | | аддитивная функция |
| hàm nhân tính | multiplicative function | | мультипликативная функция |
| hàm tuần hoàn | periodic function | | периодическая функция |
| quy nạp | induction | | индукция |