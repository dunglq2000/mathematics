## NSUCRYPTO 2022

### Lời nói đầu

Thời kì đen tối ...

Đề thi năm 2022 khá lạ và phức tạp. Bảng điểm round 2 dành cho University student cũng ảo ma không kém.

### Problem 5*. Super dependent S-box

#### Đề bài

Harry muốn tìm một super dependent S-box cho mã hóa mới. Anh ấy dùng một hoán vị liên kết chặt chẽ với mọi biến của nó và muốn ước lượng số các hoán vị như vậy.

Một hàm boolean vectorial $F(x) = (f_1(\bm{x}), f_2(\bm{x}), \ldots, f_n(\bm{x}))$, với $\bm{x} \in \mathbb{F}_2^n$, là một **hoán vị** trên $\mathbb{F}_2^n$ nếu nó là một ánh xạ one-to-one từ $\mathbb{F}_2^n$ tới $\mathbb{F}_2^n$.

Các hàm tọa độ $f_k(\bm{x})$ (là các hàm boolean từ $\mathbb{F}_2^n$ tới $\mathbb{F}_2$) được gọi là *essential depend* trên các biến $x_j$ nếu tồn tại các giá trị $b_1, b_2, \ldots, b_{j-1}, b_{j+1}, \ldots, b_n \in \mathbb{F}_2$ sao cho

$$\begin{equation*}
    f_k(b_1, b_2, \ldots, b_{j-1}, 0, b_{j+1},  \ldots, b_n) \neq f_k(b_1, b_2, \ldots, b_{j-1}, 1, b_{j+1}, \ldots, b_n)
\end{equation*}$$

Nói cách khác, essential depend trên biến $x_j$ nghĩa là trong dạng biểu diễn ANF (đa thức Zhegalkin) của hàm $f$ có sự có mặt của biến $x_j$.

````{prf:example}
Xét $n=3$. Khi đó hàm boolean $f(x_1, x_2, x_3) = x_1 x_2 \oplus x_3$ essential depend trên cả ba biến, nhưng hàm $g(x_1, x_2, x_3) = x_1 x_2 \oplus x_2 \oplus 1$ chỉ essential depend trên $x_1$ và $x_2$.
````

**Câu hỏi.** Tìm số lượng hoán vị trên $\mathbb{F}_2^n$ mà các hàm tọa độ của nó đều essential depend trên cả $n$ biến.

**Q1.** Tìm đáp án cho $n=2, 3$.

**Q2.** Tìm đáp án cho $n$ (special prize).

#### Giải

Q1 có thể được giải với SageMath. Tuy nhiên năm đó mình không dùng SageMath mà dùng Python thuần nên đáp án sai mất 😢. Đáp án cho Q1 với $n=2$ là 0 (liệt kê tất cả hàm ra) và đáp án cho $n=3$ là 24576.

Ở Q2 các team giải ra chứng minh được rằng, đáp án sẽ là một số chia hết cho $2^n \cdot n!$.

### Problem 11. A long awaited event

#### Đề bài

Bob nhận được một thông điệp

L78V8LC7GBEYEE

về một sự kiện quan trọng từ Alice.

Alice sử dụng một bảng chữ cái 37 ký tự gồm chữ cái từ A tới Z, số từ 0 tới 9 và dấu space. Các ký tự được encode như sau:

| A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |

| U | V | W | X | Y | Z | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | SPACE |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | ----- |
| 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 | 32 | 33 | 34 | 35 | 36 |

Để mã hóa Alice sử dụng hàm $f$ sao cho $f(x) = a x^2 + b x + c \pmod{37}$ với số $a, b, c$ nào đó và hàm $f$ thỏa tính chất

$$\begin{equation*}
    f(x-y) - 2 f(x) f(y) + f(1 + xy) = 1 \pmod{37} \, \text{với mọi số nguyên} \, x, y
\end{equation*}$$

**Q.** Hãy giải mã thông điệp Bob nhận được.

#### Giải

Sử dụng hàm $f$, ta có:

1. Nếu cho $y=0$ thì $f(x) - 2 f(x) \cdot f(0) + f(1) = 1 \pmod{37}$ với mọi $x \in \mathbb{Z}_{37}$.

Điều này tương đương với $(1 - 2 f(0)) \cdot f(x) = 1 - f(1) \pmod{37}$ với mọi $x \in \mathbb{Z}_{37}$.

Đẳng thức trên đúng với mọi $x \in \mathbb{Z}_{37}$ khi và chỉ khi $1 - 2 f(0) = 1 - f(1) = 0$. Suy ra $f(0) = 19$ và $f(1) = 1$.

2. Cho $x=y=1$ thì $f(2) = 1 - f(0) - 2 \cdot (f(1))^2 = 21 \pmod{37}$.

Với các cặp giá trị $(x, f(x))$ là (0, 19), (1, 1) và (2, 21) thì ta tìm lại được (bằng nội suy hoặc phép thế) đa thức $f(x) = 19 x^2 + 19 \pmod{37}$.

Khi đó, với mỗi giá trị $f(x)$ ta có hai giá trị $x$ thỏa mãn đẳng thức. Truy ngược ra đáp án khả thi cho ta thông điệp ban đầu.

| Ciphertext | L | 7 | 8 | V | 8 | L | C | 7 | G | B | E | Y | E | E |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| Plaintext 1 | <span style="color:red">N</span> | <span style="color:red">S</span> | R | <span style="color:red">C</span> | <span style="color:red">R</span> | N | <span style="color:red">P</span> | S | <span style="color:red">O</span> | B | J | L | J | J |
| | 13 | 18 | 17 | 2 | 17 | 13 | 15 | 18 | 14 | 1 | 9 | 11 | 9 | 9 |
| Plaintext 2 | Y | T | <span style="color:red">U</span> | 9 | U | <span style="color:red">Y</span> | W | <span style="color:red">T</span> | X | <span style="color:red">SPACE</span> | <span style="color:red">2</span> | <span style="color:red">0</span> | <span style="color:red">2</span> | <span style="color:red">2</span> |
| | 24 | 19 | 20 | 35 | 20 | 24 | 22 | 19 | 23 | 36 | 28 | 26 | 28 | 28 |

Theo bảng tên thì thông điệp là "NSUCRYPTO 2022".
