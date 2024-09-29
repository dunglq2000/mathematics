## SMS4

SM4 (trước đây là SMS4) là thuật toán mã hóa khối của Trung Quốc để bảo vệ mạng không dây. Thuật toán được phát triển vào năm 2006.

Phần này mình dịch từ {cite}`Tokareva1` hoặc bản dịch tiếng Anh là {cite}`cryptoeprint:2008/329`.

Input, output và độ dài khóa của SMS4 đều là $128$ bit. Thuật toán gồm $32$ vòng.

Plaintext $128$ bit sẽ được chia thành $4$ phần độ dài $32$ bit (gọi là **word**). Giả sử plaintext là $P$ có $128$ bit sẽ được biểu diễn thành

$$P = (X^0, X^1, X^2, X^3)$$

Từ khóa ban đầu là $K$, thuật toán sinh khóa sinh ra các khóa $K_0, \ldots, K_{31}$, mỗi khóa con độ dài $32$ bit.

SMS4 sử dụng **mô hình Feistel tổng quát** (hay **generalized Feistel model**).

### Mã hóa

Ở vòng thứ $i$, với $i = 0, 1, \ldots, 31$, ta tính word mới $X^{i+4}$ theo công thức

$$X^{i+4} = X^i \oplus T(X^{i+1} \oplus X^{i+2} \oplus X^{i+3} \oplus K_i)$$

```{figure} ../figures/sms4/encryption.jpg

Một vòng SMS4 (Nguồn - {cite}`Tokareva1`)
```

Ciphertext sẽ là viết ngược của bốn word ở vòng cuối cùng, nói cách khác là

$$C = (X^{35}, X^{34}, X^{33}, X^{32})$$

### Round function

Biến đổi $T$ gồm hai phần là hoán vị (không tuyến tính) $\tau$ và hoán vị (tuyến tính) $L$. Nói cách khác là $T(\cdot) = L(\tau(\cdot))$.

Hoán vị không tuyến tính có dạng

$$\tau(X) = \tau(a_0, a_1, a_2, a_3) = (\text{Sbox}(a_0), \text{Sbox}(a_1), \text{Sbox}(a_2), \text{Sbox}(a_3)),$$

với $a_i$ là các byte của $X$. Nghĩa là $X$ có $32$ bit sẽ được chia thành bốn khối độ dài $8$ bit là $a_0$, $a_1$, $a_2$ và $a_3$.

Bảng S-box có thể xem ở một trong hai tài liệu trên.

Hoán vị tuyến tính có dạng

$$L(X) = X \oplus (X \lll 2) \oplus (X \lll 10) \oplus (X \lll 18) \oplus (X \lll 24),$$

trong đó $\lll$ là phép dịch vòng bit sang trái.

### Thuật toán sinh khóa con

Khóa $K$ ban đầu ($128$ bit) được chia thành bốn word

$$K = (MK_0, MK_1, MK_2, MK_3)$$

Các khóa con $K_0, K_1, \ldots, K_{31}$ được sinh ra theo quy tắc sau. Với mỗi $i = 0, 1, \ldots, 31$ thì

$$K_i = HK_{i+4} = HK_i \oplus T'(HK_{i+1} \oplus HK_{i+2} \oplus HK_{i+3} \oplus CK_i),$$

với $HK_i = MK_i \oplus FK_i$ với $i = 0, 1, 2, 3$. Trong đó $FK$ là một mảng được định nghĩa sẵn

$$\begin{align*}
FK_0 = (\mathtt{a3b1bac6}), FK_1 = (\mathtt{56aa3350}), \\
FK_2 = (\mathtt{677d9197}), FK_3 = (\mathtt{b27022dc}).
\end{align*}$$

Hàm $T'$ khác với hàm $T$ ở trên, thay vì dùng $L$ thì dùng $L'$ có dạng

$$L'(X) = X \oplus (X \lll 13) \oplus (X \lll 23).$$

$CK$ cũng là một mảng cố định. $CK_i$ với $i = 0, 1, \ldots, 31$ là bảng sau

$$\begin{align*}
\mathtt{00070e15}, \quad \mathtt{1c232a31}, \quad \mathtt{383f464d}, \quad \mathtt{545b6269}, \\
\mathtt{70777e85}, \quad \mathtt{8c939aa1}, \quad \mathtt{a8afb6bd}, \quad \mathtt{c4cbd2d9}, \\
\mathtt{e0e7eef5}, \quad \mathtt{fc030a11}, \quad \mathtt{181f262d}, \quad \mathtt{343b4249}, \\
\mathtt{50575e65}, \quad \mathtt{6c737a81}, \quad \mathtt{888f969d}, \quad \mathtt{a4abb2b9}, \\
\mathtt{c0c7ced5}, \quad \mathtt{dce3eaf1}, \quad \mathtt{f8ff060d}, \quad \mathtt{141b2229}, \\
\mathtt{30373e45}, \quad \mathtt{4c535a61}, \quad \mathtt{686f767d}, \quad \mathtt{848b9299}, \\
\mathtt{a0a7aeb5}, \quad \mathtt{bcc3cad1}, \quad \mathtt{d8dfe6ed}, \quad \mathtt{f4fb0209}, \\
\mathtt{10171e25}, \quad \mathtt{2c333a41}, \quad \mathtt{484f565d}, \quad \mathtt{646b7279}.
\end{align*}$$

### Giải mã

Để giải mã ta dùng round function ở trên nhưng theo thứ tự ngược lại.