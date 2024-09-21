# Sự vô hạn

Tiếp theo chúng ta sẽ xem hết những bài toán hết sức thú vị cùng những lập luận cũng thú vị không kém để thấy rằng có nhiều điều bất ngờ sẽ xảy ra nếu vận dụng những lý luận chặt chẽ

## Các nghịch lý về sự vô hạn

### Nghịch lý Zeno

Zeno là nhà triết học cổ Hy Lạp nổi tiếng với bài toán *Achilles và rùa* (Achilles là anh hùng trong thần thoại Hy Lạp). Bài toán được phát biểu đơn giản như sau: 

> Nếu Achilles chạy đua và xuất phát sau con rùa thì Achilles sẽ không bao giờ bắt kịp con rùa.

Bài toán nghe thật nực cười nhưng dưới lập luận của Zeno thì bài toán sẽ trở nên "có lý". Zeno lập luận như sau: gọi $d_1$ là khoảng cách ban đầu giữa Achilles và con rùa. Achilles sẽ mất một khoảng thời gian $t_1$ để đặt tới vị trí con rùa. Tuy nhiên trong khoảng thời gian $t_1$ đó con rùa cũng đã đi một đoạn $d_2$ nào đó rồi. Dĩ nhiên $d_2$ sẽ ngắn hơn $d_1$. Nhưng nếu quá trình này lặp đi lặp lại, $d_n$ sẽ trở nên càng ngày càng nhỏ, tuy nhiên không bao giờ bằng $0$. Nói cách khác, Achilles không bao giờ bắt kịp con rùa.

Dưới góc nhìn của toán học hiện đại, điều này chưa hẳn đúng. Vì thời Zeno chưa có nhiều khái niệm lẫn công cụ về vô cực, nên người ta đã công nhận tổng vô hạn sẽ là vô hạn. Học sinh lớp 11 hiện nay khi học tới cấp số nhân lùi vô hạn sẽ biết cách tính tổng 

$$\frac{1}{10} + \frac{1}{100} + \cdots \frac{1}{10^n} = \frac{1}{9}$$

là hữu hạn.

### So sánh $\mathbb{N}$ và $\mathbb{Z}$

> Hai tập hợp $\mathbb{N}$ và $\mathbb{Z}$ là các tập vô hạn, như vậy số phần tử của tập hợp nào lớn hơn?

Câu hỏi tưởng chừng như vô vị vì nhìn vào mọi người đều thấy rằng $\mathbb{Z}$ "bao trọn" $\mathbb{N}$ (số nguyên kéo dài vô hạn về bên trái lẫn phải trong khi số tự nhiên chỉ kéo dài vô hạn về bên phải). Tuy nhiên, nhà toán học Cantor đã tìm ra một lý luận đầy *tính thuyết phục* để chứng minh rằng số phần tử của hai tập là bằng nhau.

Ta xét ánh xạ $f: \mathbb{Z} \to \mathbb{N}$ như sau:

- $f(0) = 0$;
- các số âm của $\mathbb{Z}$ biến thành các số lẻ của $\mathbb{N}$;
- các số dương của $\mathbb{Z}$ thì biến thành các số chẵn của $\mathbb{N}$.

Ví dụ $f(-1) = 1$, $f(-2) = 3$, $f(-3) = 5$ và cứ như vậy tăng lên. Tương tự với số dương $f(1) = 2$, $f(2) = 4$. Ta có công thức

$$z = f(n) = \begin{cases} 2n, & \quad \text{nếu } n \geqslant 0 \\ -1-2n, & \quad \text{nếu } n < 0\end{cases}$$

Như vậy $f$ là đơn ánh vì hai phần tử khác nhau của $\mathbb{Z}$ sẽ cho ra hai phần tử khác nhau thuộc $\mathbb{N}$. Tương tự $f$ cũng là toàn ánh vì mọi phần tử thuộc $\mathbb{N}$ đều có một phần tử từ $\mathbb{Z}$ biến thành. Như vậy $f$ là song ánh. Vậy số phần tử của $\mathbb{N}$ và $\mathbb{Z}$ bằng nhau.

Bằng lập luận tương tự cũng có thể chứng minh số phần tử của $\mathbb{Q}$ bằng số phần tử của $\mathbb{N}$. Những lập luận này đã gây ra tiếng vang lớn vào thời đó.

Từ đây tập hợp vô hạn có thể chia ra **đếm được** (countable) và **không đếm được** (uncountable). Tiếp theo ta định nghĩa hai dạng tập hợp này.

1. Tập hợp được gọi là **đếm được** khi tồn tại song ánh từ nó tới $\mathbb{N}$.
2. Tập hợp được gọi là **không đếm được** khi nó không phải là tập đếm được.

### Định lý về $\mathbb{R}$

````{prf:theorem}
Tập hợp số thực $$\mathbb{R}$$ là tập không đếm được
````

```{admonition} **Chứng minh**
:class: danger

Cantor đưa ra hai phương pháp chứng minh và cả hai đều độc đáo. Chúng ta cần một nhận xét sau:

> Khoảng $(0, 1)$ là tương đương với tập $\mathbb{R}$.

Chúng ta có thể xây dựng một song ánh từ $\mathbb{R}$ tới $(0, 1)$, ví dụ $f(x) = \dfrac{e^x}{e^x+1}$.

**Phương án 1:** Phương pháp chéo hóa (diagonalization).

Xét ánh xạ

$$\begin{align*}
    & 0 \to 0,a_{0, 0}a_{0, 1}a_{0, 2} \cdots \\
    & 1 \to 0,a_{1, 0}a_{1, 1}a_{1, 2} \cdots \\
    & 2 \to 0,a_{2, 0}a_{2, 1}a_{2, 2} \cdots \\
    & \cdots
\end{align*}$$

Ta chứng minh ánh xạ này không phải toàn ánh. Xét số $y = 0,b_0 b_1 b_2 \cdots$, với $b_i \neq a_{i, i}$ với mọi $i$, tức là trên đường chéo của các số trên ta chọn số $b_i$ khác với số trên đường chéo. Như vậy số $y$ này có chữ số ở vị trí 0 khác $f(0)$, chữ số ở vị trí 1 khác $f(1)$, vân vân, nên không tìm được số $n$ nào mà $f(n) = y$. Suy ra $f$ không phải toàn ánh và từ đó không phải song ánh.

**Phương án 2.** Phương pháp dãy các đoạn thẳng đóng bị chặn lồng vào nhau (sequence of closed bounded nested).

Giả sử đoạn $(0, 1)$ đếm được. Khi đó ta có thể liệt kê các phần tử của đoạn là $I = \{ x_1, x_2, \ldots \}$.

Từ tập $I$ ta lấy ra một đoạn con $I_1$ sao cho $x_1 \not\in I_1$.

Tiếp theo, từ tập $I_1$ ta lấy ra một đoạn con $I_2$ sao cho $x_2 \not\in I_2$.

Tiếp tục như vậy, ta lấy ra các đoạn con

$$ \cdots \subset I_n \subset \cdots \subset I_2 \subset I_1 \subset I$$

với $x_n \not\in I_n$ với mọi $n \in \mathbb{N}$. 

Theo định lý về các đoạn thẳng đóng bị chặn lồng vào nhau thì giao của chúng không rỗng, tức là tồn tại số $x$ thuộc giao giao của các tập $I_1, \ldots, I_n$. Phần tử $x \in I_n$ với mọi $n$. Do $x_1 \not\in I_n$ và $x \in I_n$ nên $x \neq x_n$ với mọi $n$, tức là không nằm trong tập $I$. Điều này mâu thuẫn với giả sử đoạn $(0, 1)$ đếm được. Suy ra đoạn $(0, 1)$ là tập không đếm được.
```
