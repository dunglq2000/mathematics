## NSUCRYPTO 2021

### Problem 4 (R1). Elliptic curve points

#### Đề bài

Đặt $E / \mathbb{F}_p$ là đường cong elliptic với dạng Weiertrass. Đường cong này có phương trình $y^2 = x^3 + ax + b$, với $a, b \in \mathbb{F}_p$ và $4a^3 + 27a^2 \neq 0$. Các điểm affine trong $E$ và điểm vô cực $\mathcal{O}$ tạo thành một nhóm Abel, đặt

$$\begin{equation*}
    E(\mathbb{F}_p) = \{ (x, y) \in \mathbb{F}_p^2 : y^2 = x^3 + ax + b \} \cup \{ \mathcal{O} \}
\end{equation*}$$

Giả sử $b=0$. Gọi $R \in E(\mathbb{F}_p)$ là điểm với order lẻ và $R \neq \mathcal{O}$. Xét $H = \langle R \rangle$ là subgroup sinh bởi $R$.

Giúp Alice chứng minh rằng nếu $(u, v) \in H$ thì $u$ là số chính phương modulo $p$.

#### Giải

Gọi $Q = (x', y') \in H$. Do $R$ có order lẻ nên $Q$ cũng có order lẻ (order của phần tử trong subgroup chia hết order của subgroup đó).

Giả sử order của $Q$ là $n$ lẻ. Xét điểm $P = \dfrac{n+1}{2} Q$, do $n$ lẻ nên dễ thấy $P \in H$. Đặt $P = (x, y)$.

Do $2P = (n+1) Q = Q$ (do $Q$ có order là $n$) nên theo công thức cộng hai điểm trên elliptic ta có

$$\begin{align*}
    x' & = \left(\frac{3x^2 + a}{2y}\right) - 2x \\
       & = \frac{9x^4 + 6x^2 a + a^2 - 8x(x^3 + ax)}{(2y)^2} \\
       & = \frac{x^4 - 2x^2 a + a^2}{(2y)^2} \\
       & = \left(\frac{x^2-a}{2y}\right)
\end{align*}$$

Biểu thức cuối cho thấy rằng $x'$ là số chính phương modulo $p$ (đpcm).

### Problem 9. 2021-bit key

#### Đề bài

Một generator dùng pseudo-random để sinh ra một dãy bit (0 hoặc 1) từng bước một. Để bắt đầu generator, một người phải trả 1 *nsucoin* và generator sẽ sinh ngẫu nhiên một bit (dãy bit độ dài bằng 1). Khi đó, với một dãy $S$ được sinh có độ dài $l$, $l \geqslant 1$, một trong các động tác sau được thực hiện:

1. Một dãy ngẫu nhiên độ dài 4 được thêm vào $S$, khi đó dãy $S'$ có độ dài $l + 4$. Việc này tốn 2 *nsucoin*.
2. Một dãy ngẫu nhiên độ dài $2l$ được thêm vào $S$, khi đó dãy $S'$ có độ dài $3l$. Việc này tốn 5 *nsucoin*.

Bob cần sinh độ dài chính xác 2021 bit. Số lượng *nsucoin* nhỏ nhất để thực hiện việc này là bao nhiêu?

#### Giải

Dễ thấy rằng khi $l > 2$ thì sử dụng động tác thứ hai khiến độ dài dãy tăng lên rất nhanh như lại tốn thêm coin.

Như vậy khi $l > 6$ mình sẽ chứng minh rằng động tác thứ hai hiệu quả hơn.

Để ý rằng nếu mình sử dụng động tác thứ nhất ba lần liên tiếp, khi đó từ dãy có độ dài $l$ mình thu được dãy mới độ dài $l + 4 + 4 + 4 = l + 12$ và việc này tốn 6 *nsucoin*.

Trong khi đó, nếu mình dùng động tác thứ hai một lần thì từ dãy độ dài $l$ mình thu được dãy độ dài $3l$ và tốn 5 *nsucoin*.

Mình muốn $3l > l + 12$ vì mình đã có $3l$ tương ứng 5 *nsucoin* và $l + 12$ tương ứng 6 *nsucoin*. Như vậy $l > 6$.

Chiến thuật lúc này là mình sẽ dùng động tác thứ hai để triple độ dài bất cứ lúc nào có thể. Nói cách khác là khi đi ngược từ 2021 về 0 thì khi nào số chia hết cho 3, mình sẽ dùng động tác sau, không thì dùng động tác đầu.

Quá trình sẽ diễn ra theo bảng sau.

| Phép tính | Số *nsucoin* thu được |
| --------- | --------------------- |
| $2021 - 4 = 2017$ | 2 *nsucoin* |
| $2017 - 4 = 2013$ | 2 *nsucoin* |
| $2013 / 3 = 671$ | 5 *nsucoin* |
| $671 - 4 = 667$ | 2 *nsucoin* |
| $667 - 4 = 663$ | 2 *nsucoin* |
| $663 / 3 = 221$ | 5 *nsucoin* |
| $221 - 4 = 217$ | 2 *nsucoin* |
| $217 - 4 = 213$ | 2 *nsucoin* |
| $213 / 3 = 71$ | 5 *nsucoin* |
| $71 - 4 = 67$ | 2 *nsucoin* |
| $67 - 4 = 63$ | 2 *nsucoin* |
| $63 / 3 = 21$ | 5 *nsucoin* |

Từ 21 trở đi không thể áp dụng quy tắc trên nữa vì theo chứng minh trên chiến thuật chỉ hiệu quả với $l > 6$.

Mình khai triển $21 = 1 + 4 + 4 + 4 + 4 + 4$, thực hiện 4 phép trừ (động tác đầu) tốn $5 \cdot 2 = 10$ *nsucoin* và trừ 1 tốn 1 *nsucoin*.

Như vậy tổng số *nsucoin* nhỏ nhất cần là 47.

