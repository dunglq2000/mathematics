## Nhập môn phá mã vi sai

```{contents}
:depth: 2
```

[^aking]: http://theamazingking.com/crypto-diff.php

Phần này mình tham khảo ở [^aking]. Bạn này viết khá nhiều bài nhập môn cryptanalysis trên block cipher nên rất tốt để tham khảo.

### Differential (vi sai)

````{prf:definition}
Gọi $\mathbb{F}_2^n$ và $\mathbb{F}_2^m$ là hai không gian vector trên $\mathbb{F}_2$ với số chiều lần lượt là $n$ và $m$. Gọi $S$ là ánh xạ từ $\mathbb{F}_2^n$ tới $\mathbb{F}_2^m$. Với mỗi vector $\bm{a}, \bm{b} \in \mathbb{F}_2^n$, ta nói **input differential** của $S$ là $\delta = \bm{a} \oplus \bm{b}$ và **output differential** của $S$ là $\Delta = S(\bm{a}) \oplus S(\bm{b})$, trong đó $\oplus$ là phép XOR.
````

Trên thực tế, nếu trường được xét không phải $\mathbb{F}_2$ mà là một trường $\mathbb{F}$ bất kì thì input differential là $\bm{b} - \bm{a}$ và output differential là $S(\bm{b}) - S(\bm{a})$. Trong mật mã chúng ta thường hay làm việc trên các không gian vector nhị phân nên phép trừ cũng chính là phép cộng (XOR) trên $\mathbb{F}_2$.

Ánh xạ $S$ thường được sử dụng trong S-box là ánh xạ không tuyến tính, nghĩa là chúng ta không có tính chất $S(\bm{a} \oplus \bm{b}) = S(\bm{a}) \oplus S(\bm{b})$. Tuy nhiên khi phân tích phân bố của $\delta = \bm{a} \oplus \bm{b}$ và $\Delta = S(\bm{a}) \oplus S(\bm{b})$ ta có thể trích ra các thông tin phục vụ tấn công. Do sử dụng các thông tin thống kê từ differential nên cách tấn công này được gọi là **differential attack** (hay **phá mã vi sai**).

### Toy cipher

1. Độ dài khối là $4$ bit.
2. Độ dài khóa là $8$ bit.

Mình gọi plaintext $4$ bit là $P$ và khóa $8$ bit là $K = K_0 \Vert K_1$, trong đó $K_0$ và $K_1$ có $4$ bit và $\Vert$ là toán tử ghép chuỗi.

S-box của toy cipher là ánh xạ $\mathbb{F}_2^4$ tới $\mathbb{F}_2^4$ theo bảng sau:

| $\bm{x}$ | $0$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ | $7$ | $8$ | $9$ | $10$ | $11$ | $12$ | $13$ | $14$ | $15$ |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| $S(\bm{x})$ | $3$ | $14$ | $1$ | $10$ | $4$ | $9$ | $5$ | $6$ | $8$ | $11$ | $15$ | $2$ | $13$ | $12$ | $0$ | $7$ |

Quá trình mã hóa mỗi khối plaintext $4$ bit $P$ thành ciphertext $C$ cũng $4$ bit là:

$$P \to P \oplus K_0 \to S(P \oplus K_0) \to S(P \oplus K_0) \oplus K_1 = C$$

### Phân tích vi sai

Tiếp theo chúng ta phân tích sự phân bố vi sai của S-box và biểu diễn thành bảng. Trong bảng này, phần tử ở hàng $i$ và cột $j$ thể hiện số lượng cặp $(\bm{a}, \bm{b}) \in \mathbb{F}_2^4 \times \mathbb{F}_2^4$ sao cho $\bm{a} \oplus \bm{b} = i$ và $S(\bm{a} \oplus \bm{b}) = j$.

| | $0$ | $1$ | $2$ | $3$ | $4$ | $5$ | $6$ | $7$ | $8$ | $9$ | $10$ | $11$ | $12$ | $13$ | $14$ | $15$ |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| $0$ | <span style="color:red">16</span> |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |  0 | 0 |  0 |  0 |
| $1$ |  0 |  2 |  0 |  4 |  0 |  0 |  0 |  2 |  0 |  0 |  0 |  2 |  0 |  <span style="color:red">6</span> |  0 |  0 |
| $2$ |  0 |  2 |  2 |  0 |  2 |  0 |  0 |  2 |  0 |  2 |  0 |  2 |  0 |  2 |  0 |  2 |
| $3$ |  0 |  0 |  2 |  0 |  2 |  0 |  0 |  0 |  0 |  2 |  4 |  0 |  4 |  0 |  0 |  2 |
| 4 |  0 |  0 |  0 |  0 |  2 |  4 |  0 |  <span style="color:red">6</span> |  0 |  0 |  0 |  0 |  2 |  0 |  0 |  2 |
| 5 |  0 |  0 |  2 |  0 |  2 |  0 |  2 |  2 |  2 |  0 |  4 |  0 |  0 |  0 |  0 |  2 |
| 6 |  0 |  0 |  2 |  2 |  0 |  2 |  2 |  0 |  4 |  0 |  0 |  0 |  2 |  0 |  2 |  0 |
| 7 |  0 |  0 |  0 |  2 |  0 |  2 |  0 |  0 |  2 |  0 |  0 |  4 |  0 |  0 |  2 |  4 |
| 8 |  0 |  2 |  0 |  0 |  0 |  <span style="color:red">6</span> |  0 |  0 |  2 |  2 |  0 |  2 |  0 |  0 |  2 |  0 |
| 9 |  0 |  0 |  2 |  2 |  2 |  2 |  4 |  0 |  4 |  0 |  0 |  0 |  0 |  0 |  0 |  0 |
| 10 | 0 |  2 |  0 |  0 |  2 |  0 |  0 |  0 |  2 |  2 |  2 |  0 |  4 |  0 |  2 |  0 |
| 11 | 0 |  4 |  2 |  2 |  0 |  0 |  0 |  0 |  0 |  4 |  2 |  2 |  0 |  0 |  0 |  0 |
| 12 | 0 |  2 |  4 |  0 |  2 |  0 |  0 |  0 |  0 |  0 |  2 |  0 |  2 |  2 |  2 |  0 |
| 13 | 0 |  2 |  0 |  2 |  0 |  0 |  2 |  2 |  0 |  2 |  2 |  0 |  0 |  0 |  0 |  4 |
| 14 | 0 |  0 |  0 |  2 |  0 |  0 |  2 |  0 |  0 |  2 |  0 |  4 |  2 |  4 |  0 |  0 |
| 15 | 0 |  0 |  0 |  0 |  2 |  0 |  4 |  2 |  0 |  0 |  0 |  0 |  0 |  2 |  <span style="color:red">6</span> |  0 |

Chúng ta quan tâm tới những hàng có nhiều giá trị $0$ và có một phần tử lớn nhất.

Cụ thể thì ở bảng này:

1. Nếu input differential là $0$ thì output differential là $0$ với xác suất $16 / 16 = 1$.
2. Nếu input differential là $1$ thì output differential là $13$ với xác suất $6 / 16$.
3. Nếu input differential là $4$ thì output differential là $7$ với xác suất $6 / 16$.
4. Nếu input differential là $8$ thì output differential là $5$ với xác suất $6 / 16$.
5. Nếu input differential là $15$ thì output differential là $14$ với xác suất $6 / 16$.

Khi input differential là $0$, nói cách khác là $\bm{a} \oplus \bm{b} = 0$, tương đương với $\bm{a} = \bm{b}$. Suy ra $S(\bm{a}) = S(\bm{b})$ nên output differential luôn là $0 = S(\bm{a}) \oplus S(\bm{b})$. Tính chất này không hữu dụng.

Tiếp theo, giả sử ta mã hóa plaintext $P_1$ và nhận được ciphertext tương ứng là $C_1$.

Tương tự ta mã hóa plaintext $P_1'$ và nhận được ciphertext tương ứng là $C_1'$.

Theo cấu trúc cipher, $P_1 \oplus K_0$ và $P_1' \oplus K_0$ sẽ là các đầu vào của S-box. Do đó input differential là

$$\delta = (P_1 \oplus K_0) \oplus (P_1' \oplus K_0) = P_1 \oplus P_1'.$$

Điều này có nghĩa là input differential không phụ thuộc vào khóa và đây là tính chất quan trọng cho phá mã vi sai.

Theo quan sát số 2 về bảng phân bố vi sai ở trên, nếu input differential là $1$ thì output differential là $13$ với xác suất $6 / 16$.

Giả sử ta chọn các plaintext $P_1$ và $P_1'$ sao cho $P_1 \oplus P_1' = 1$.

Đặt $I_1 = S(P_1 \oplus K_0)$ và $I_1' = S(P_1' \oplus K_0)$. Khi đó output differential của S-box là $I_1 \oplus I_1'$ và bằng $13$  với xác suất $6 / 16$.

Để ý rằng $C_1 = I_1 \oplus K_1$ và $C_1' = I_1' \oplus K_1$ nên

$$C_1 \oplus C_1' = (I_1 \oplus K_1) \oplus (I_1' \oplus K_1) = I_1 \oplus I_1'$$

chính là output differential.

````{prf:remark}
Nếu hai plaintext $P_1$ và $P_1'$ thỏa mãn $P_1 \oplus P_1' = 1$ thì hai ciphertext tương ứng $C_1$ và $C_1'$ sẽ cho giá trị $C_1 \oplus C_1' = 13$ với xác suất $6 / 16$.
````

Nói cách khác, trung bình $16$ cặp plaintext mà $P_1 \oplus P_1' = 16$ thì sẽ có $6$ cặp cho kết quả $C_1 \oplus C_1' = 13$.

### Chosen plaintext

Dựa vào nhận xét trên, chiến thuật phá mã vi sai thực hiện như sau:

1. Chọn ngẫu nhiên plaintext $P_1$ và tính $P_1' = P_1 \oplus 1$.
2. Mã hóa $P_1$ thu được $C_1$, mã hóa $P_1'$ thu được $C_1'$.
3. Nếu $C_1 \oplus C_1' = 13$ thì ta đã tìm được một cặp plaintext "tốt". Nếu không thì ta quay lại bước 1.

Xác suất $6 / 16$ đảm bảo rằng việc tìm kiếm sẽ không mất thời gian vì xác suất này khá lớn so với phần còn lại :)))

Khi chúng ta đã tìm được cặp plaintext $(P_1, P_1')$ mà $C_1 \oplus C_1' = 13$, chúng ta đã sẵn sàng khôi phục khóa con $K_0$.

Đầu tiên, ta liệt kê tất cả cặp $(\bm{a}, \bm{b}) \in \mathbb{F}_2^4 \times \mathbb{F}_2^4$ sao cho $\bm{a} \oplus \bm{b} = 1$ và $S(\bm{a}) \oplus S(\bm{b}) = 13$. Các cặp đó là

$$\mathcal{S}_0 = \{ (0, 1), (1, 0), (4, 5), (5, 4), (10, 11), (11, 10) \}.$$

Do phép XOR có tính đối xứng nên tập $\mathcal{S}_0$ cũng có những cặp đối xứng. Do đó ta chỉ cần lấy phần tử đầu của mỗi cặp và đặt

$$\mathcal{A} = \{ 0, 1, 4, 5, 10, 11 \}.$$

Mỗi phần tử $\bm{a} \in \mathcal{A}$ có tính chất $S(\bm{a}) \oplus S(\bm{a} \oplus 1) = 13$.

Theo cấu trúc của toy cipher thì $S(P_1 \oplus K_0) \oplus S(P_1' \oplus K_0) = 13$.

Như vậy $\bm{a} = P_1 \oplus K_0$ và $\bm{a} \oplus 1 = P_1' \oplus K_0$. Từ đây ta tìm được các khả năng có thể có của khóa con $K_0$ ứng với mỗi giá trị $\bm{a}$.

Với mỗi giá trị $K_0$, ta tính được $K_1 = C_1 \oplus S(P_1 \oplus K_0)$. Do $\mathcal{A}$ có $6$ phần tử nên ta sẽ có $6$ trường hợp khóa $K = K_0 \Vert K_1$.

Để tìm ra khóa ta có thể thử mã hóa $P_1$ với từng khóa. Nếu kết quả là $C_1$ thì ta đã khôi phục đúng khóa.

Differential cryptanalysis ở toy cipher đã giảm số lượng khóa cần thử từ $2^8 = 256$ trường hợp xuống còn $6$ trường hợp.
