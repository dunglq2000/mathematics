## AES

AES biến đổi theo khối $128$ bit, sử dụng mô hình mạng SPN.

Bốn phép biến đổi chính là Add Round Key, Substitute Bytes, Shift Rows và Mix Columns.

Quá trình giải mã sử dụng phép biến đổi ngược của bốn phép biến đổi trên là Inverse Sub Bytes, Inverse Shift Rows, Inverse Mix Columns. Đối với Add Round Key bản thân là phép XOR nên phép biến đổi ngược là chính nó.

AES hỗ trợ key với các kích thước: $128$ bit, $192$ bit và $256$ bit. 

Đối với kích thước khóa $128$ bit, AES dùng hàm Expand Key để mở rộng khóa thành $44$ word, mỗi word có $32$ bit, với key $128$ bit thành $11$ cụm khóa con. Mỗi $4$ word làm tham số cho một phép Add Round Key.

Mỗi block bản rõ $16$ byte $p_0, p_1, \ldots, p_{15}$ được tổ chức dưới dạng một ma trận $4 \times 4$ (gọi là **ma trận state**)

```{figure} ../figures/aes/state.jpg
```  

1. Các phép biến đổi Add Round Key, Substitute Bytes, Shift Rows, Mix Columns được thực hiện trên ma trận $4 \times 4$ này.
2. Các phép tính số học trong AES được thực hiện trong $\mathrm{GF}(2^8)$ với đa thức tối giản là $f(x) = x^8 + x^4 + x^3 + x + 1$.

### Substitute Bytes

#### Substitute Bytes

Ta sử dụng một bảng tra cứu $16 \times 16$ (S-box).

1. Điền các số từ 0 tới 255 theo từng hàng
2. Thay thế mối byte trong bảng bằng nghịch đảo trong $\mathrm{GF}(2^8)$. Quy ước $(00)^{-1} = 00$
3. Với mỗi byte trong bảng, ta ký hiệu 8 bit là $b_7 b_6 b_5 b_4 b_3 b_2 b_1 b_0$. Thay thế mỗi $b_i$ bằng $b_i'$ như sau

$$b'_i = b_i \oplus b_{(i+4) \bmod 8} \oplus b_{(i+5) \bmod 8} \oplus b_{(i+6) \bmod 8} \oplus b_{(i+7) \bmod 8} \oplus c_i$$

với $c_i$ là bit thứ $i$ của số $0x63$.

Việc tính trên tương đương với phép nhân trên ma trận $\mathrm{GF}(2)$ là $B' = XB + C$

$$\begin{bmatrix}
    b'_0 \\ b'_1 \\ b'_2 \\ b'_3 \\ b'_4 \\ b'_5 \\ b'_6 \\ b'_7
\end{bmatrix} = 
\begin{bmatrix}
    1 & 0 & 0 & 0 & 1 & 1 & 1 & 1 \\
    1 & 1 & 0 & 0 & 0 & 1 & 1 & 1 \\
    1 & 1 & 1 & 0 & 0 & 0 & 1 & 1 \\
    1 & 1 & 1 & 1 & 0 & 0 & 0 & 1 \\
    1 & 1 & 1 & 1 & 1 & 0 & 0 & 0 \\
    0 & 1 & 1 & 1 & 1 & 1 & 0 & 0 \\
    0 & 0 & 1 & 1 & 1 & 1 & 1 & 0 \\
    0 & 0 & 0 & 1 & 1 & 1 & 1 & 1
\end{bmatrix} 
\begin{bmatrix}
    b_0 \\ b_1 \\ b_2 \\ b_3 \\ b_4 \\ b_5 \\ b_6 \\ b_7
\end{bmatrix} + 
\begin{bmatrix}
    1 \\ 1 \\ 0 \\ 0 \\ 0 \\ 1 \\ 1 \\ 0
\end{bmatrix}$$

Ma trận $X$ là ma trận khả nghịch, do đó phép biến đổi S-box là song ánh (one-to-one và onto mapping).

Dựa vào bảng S-box, Substitute Bytes thực hiện như sau: mỗi byte trong ma trận state $S$ dưới dạng thập lục phân là $xy$ sẽ được thay bằng giá trị ở hàng $x$ và cột $y$ của S-box.

#### Inverse Sub Bytes

Ta cần xây dựng bảng Inverse Sub Bytes (IS-box).

Việc xây dựng bảng này giống với bảng S-box ở bước 1 và 2. Tại bước 3:

$$b_i = b'_{(i+2) \bmod 8} \oplus b'_{(i+5) \bmod 8} \oplus b'_{(i+7) \bmod 8} \oplus d_i$$

với $d_i$ là bit thứ $i$ của số $0x05$.

#### Ý nghĩa của Substitute Bytes

Bảng S-box dùng để chống lại known-plaintext và là bước duy nhất trong bốn bước không có quan hệ tuyến tính.

### Shift Rows

#### Shift Rows

Trong Shift Rows, các dòng của ma trận state được biến đổi như sau:

1. Dòng thứ nhất giữ nguyên
2. Dòng 2 dịch vòng trái 1 ô
3. Dòng 3 dịch vòng trái 2 ô
4. Dòng 4 dịch vòng trái 3 ô

```{figure} ../figures/aes/shiftrows.jpg
```

#### Inverse Shift Rows

Các dòng thứ 2, 3, 4 dịch phải tương ứng 1, 2, 3 ô.

#### Ý nghĩa

Xáo trộn các byte để tạo ra các cột cho Mix Columns.

### Mix Columns

#### Mix Columns

Mix cols biến đổi từng cột của ma trận state một cách độc lập bằng phép nhân đa thức. Giả sử cột đầu tiên của ma trận state viết dưới dạng đa thức là

$$f(z) = s_{00} z^3 + s_{10} z^2 + s_{20} z + s_{30}$$

với $z \in \mathrm{GF}(2^8)$

Khi đó $f(z)$ sẽ được nhân với $a(z) = 3z^3 + z^2 + z + 2$, lưu ý rằng tất cả hệ số, phép cộng và nhân thực hiện trên $\mathrm{GF}(2^8)$, và sau đó modulo cho $n(z) = z^4 + 1$.

Bốn byte hệ số của kết quả sẽ thay thế cho bốn byte tương ứng trong cột. Nếu viết dưới dạng ma trận, ta có

$$\begin{bmatrix}
    s'_{00} \\ s'_{10} \\ s'_{20} \\ s'_{30}
\end{bmatrix} = \begin{bmatrix}
    02 & 03 & 01 & 01 \\
    01 & 02 & 03 & 01 \\
    01 & 01 & 02 & 03 \\
    03 & 01 & 01 & 02
\end{bmatrix} 
\begin{bmatrix}
    s_{00} \\ s_{10} \\ s_{20} \\ s_{30}
\end{bmatrix}$$

Lưu ý rằng các số $01$, $02$, $03$ tuy viết dưới dạng thập phân nhưng khi tính toán phải ở dạng $\mathrm{GF}(2^8)$. Việc sử dụng $1$, $2$, $3$ giúp tăng tốc độ tính toán vì $1$ và $2$ chỉ cần phép dịch bit, còn $3$ là XOR của $1$ và $2$.

#### Inverse Mix Columns

Lúc này ma trận nghịch đảo có dạng

$$\begin{bmatrix}
    \text{0E} & \text{0B} & \text{0D} & \text{09} \\
    \text{09} & \text{0E} & \text{0B} & \text{0D} \\
    \text{0D} & \text{09} & \text{0E} & \text{0B} \\
    \text{0B} & \text{0D} & \text{09} & \text{0E}
\end{bmatrix}$$

#### Ý nghĩa

Mỗi cột mới chỉ phụ thuộc cột ban đầu. Cùng với sự kết hợp Shift Rows sau một vài vòng biến đổi (cụ thể là $2$, các bạn có thể thử chứng minh), $128$ bit kết quả phụ thuộc vào tất cả $128$ bit ban đầu. Từ đó tạo ra tính khuếch tán (diffusion).

### Add Round Key

#### Add Round Key

$128$ bit của ma trận state được XOR với $128$ bit của khóa con từng vòng ($4$ dword $32$ bit). Phép biến đổi ngược của Add Round Key là chính nó.

#### Ý nghĩa

Sự kết hợp với khóa tạo ra tính làm rối (confusion).

### Expand Key

#### Expand Key

Input của thao tác Expand Key là $16$ byte ($4$ word) của khóa, sinh ra một mảng $44$ word ($176$ byte) sử dụng cho $11$ vòng AES, mỗi vòng $4$ word.

```{figure} ../figures/aes/expandkey.jpg
```

Từ 4 word đầu vào $w_0 w_1 w_2 w_3$, lần lặp đầu sinh ra $w_4 w_5 w_6 w_7$, lần lặp thứ hai sinh ra $w_8 w_9 w_{10} w_{11}$, \dots

````{prf:algorithm}
1. if $i \bmod 4 = 0$
    1. $g \gets SubWord(RotWord(w_{i-1})) \oplus Rcon[i/4]$
    2. $w_i = w_{i-4} \oplus g$
2. else
    1. $w_i = w_{i-4} \oplus w_{i-1}$
3. endif
````

Trong đó, 

1. $RotWord$ dịch vòng trái $1$ bit, nghĩa là $b_0 b_1 b_2 \rightarrow b_1 b_2 b_0$.
2. $SubWord$ thay mỗi byte trong word bằng bảng S-box
3. $Rcon$ là một mảng hằng số gồm $10$ word tương ứng với $10$ vòng AES. $4$ byte của một phần tử $Rcon[j]$ là $RC[j], 0, 0, 0$ với $RC[j]$ là mảng $10$ byte như sau

| $j$ | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| --- | - | - | - | - | - | - | - | - | - | -- |
| $RC[j]$ | 1 | 2 | 4 | 8 | 10 | 20 | 40 | 80 | 18 | 36 |

#### Ý nghĩa của Expand Key

Dùng để chống lại known-plaintext (giống Sub Bytes dùng S-box). Đặc điểm của Expand Key gồm:

- Biết một số bit của khóa hay khóa con không thể tính được các bit còn lại
- KHÔNG THỂ tính ngược
- Khuếch tán: mỗi bit của khóa chính tác động lên tất cả khóa con

### Kết luận

Mã hóa AES đơn giản và có thể chạy trên các chip 8 bit.

AES cung cấp ba biến thể cho độ dài khóa là:

- $128$ bit: $44$ word $4$ byte cho $10$ vòng ($11$ lần ARK)
- $192$ bit: $52$ word $4$ byte cho $12$ vòng ($13$ lần ARK)
- $256$ bit: $60$ word $4$ byte cho $14$ vòng ($15$ lần ARK)

### Về phép Mix Columns

Sau đây mình sẽ nói về việc phép nhân trên đa thức có hệ số trong $\mathrm{GF}(2^8)$ lại tương đương với phép nhân ma trận trong Mix Columns ở trên.

Giả sử ma trận trạng thái trước khi bước vào phép tính Mix Column của AES
là

$$\begin{equation*}
    \begin{pmatrix}
        c_0 & c_1 & c_2 & c_3 \\
        c_4 & c_5 & c_6 & c_7 \\
        c_8 & c_9 & c_{10} & c_{11} \\
        c_{12} & c_{13} & c_{14} & c_{15}
    \end{pmatrix}
\end{equation*}$$

Phép tính Mix Column lấy mỗi cột của ma trận trạng thái trên làm tham số cho đa thức với hệ số trong $\mathrm{GF}(2^8)$ và nhân với đa thức $c(z) = 2 + z + z^2 + 3z^3$ rồi modulo cho $z^4 + 1$.

Giả sử với cột đầu tiên, ta viết hệ số theo thứ tự bậc tăng dần $d(z) = c_0 + c_4 z + c_8 z^2 + c_{12} z^3$.

Tính trong $\mathrm{GF}(2^8)$

$$\begin{align*}
    c(z) \cdot d(z) = & (2 + z + z^2 + 3 z^3) \cdot (c_0 + c_4 z + c_8 z^2 + c_{12} z^3) \\
    = & 2 c_0 + 2 c_4 z + 2 c_8 z^2 + 2 c_{12} z^3 \\
    + & c_0 z + c_4 z^2 + c_8 z^3 + c_{12} z^4 \\
    + & c_0 z^2 + c_4 z^3 + c_8 z^4 + c_{12} z^5 \\
    + & 3 c_0 z^3 + 3 c_4 z^4 + 3 c_8 z^5 + 3 c_{12} z^6 \\
    = & 2 c_0 + (2 c_4 + c_0) z + (2 c_8 + c_4 + c_0) z^2 \\
    + & (2 c_{12} + c_8 + c_4 + 3 c_0) z^3 + (c_{12} + c_8 + 3 c_4) z^4 \\
    + & (c_{12} + 3 c_8) z^5 + 3 c_{12} z^6
\end{align*}$$

Trong $\mathrm{GF}(2^8)$ thì mọi phần tử đều có tính chất $2 x^n = 0$, tương đương với $x^n = -x^n$. Do đó

$$\begin{align*}
    & z^6 \pmod{z^4 + 1} \equiv -z^2 \equiv z^2 \\
    & z^5 \pmod{z^4 + 1} \equiv -z \equiv z \\
    & z^4 \pmod{z^4 + 1} \equiv -1 \equiv 1
\end{align*}$$

Suy ra

$$\begin{align*}
    c(z) \cdot d(z) = & 2 c_0 + (2 c_4 + c_0) z + (2 c_8 + c_4 + c_0) z^2 \\
    + & (2 c_{12} + c_8 + c_4 + 3 c_0) z^3 + (c_{12} + c_8 + 3 c_4) \\
    + & (c_{12} + 3 c_8) z + 3 c_{12} z^2 \\
    = & (c_{12} + c_8 + 3 c_4 + 2 c_0) + (c_{12} + 3 c_8 + 2 c_4 + c_0) z \\
    + & (3 c_{12} + 2 c_8 + c_4 + c_0) z^2 + (2 c_{12} + c_8 + c_4 + 3 c_0) z^3
\end{align*}$$

Như vậy xét hệ số lần lượt trước 1, $z$, $z^2$ và $z^3$ thì tương đương với phép
nhân ma trận

$$\begin{equation*}
    \begin{pmatrix}
        2 & 3 & 1 & 1 \\
        1 & 2 & 3 & 1 \\
        1 & 1 & 2 & 3 \\
        3 & 1 & 1 & 2
    \end{pmatrix} \cdot
    \begin{pmatrix}
        c_0 \\ c_4 \\ c_8 \\ c_{12}
    \end{pmatrix}
\end{equation*}$$

Đây chính là kết quả cần tìm.
