## TJCTF 2024 phần 3

Mình dành hẳn một phần cho một bài vì bài này khá dài và phức tạp.

Đây cũng là bài viết đầu tiên của mình về một phương pháp tấn công cực kì phổ biến là differential attack (phá mã vi sai).

### tetraethyllead

```python
# server.py
#!/usr/local/bin/python3 -u

import secrets
import hashlib
from Crypto.Util.number import bytes_to_long, long_to_bytes

def rrot(word, i):
    i %= 32
    word = word & ((1 << 32) - 1)
    return ((word >> i) | (word << (32 - i))) & ((1 << 32) - 1)

def lrot(word, i):
    i %= 32
    word = word & ((1 << 32) - 1)
    return ((word << i) | (word >> (32 - i))) & ((1 << 32) - 1)
    

def get_sbox(word):
    
    Sbox = [17, 16, 19, 18, 21, 20, 23, 22, 25, 24, 27, 26, 29, 28, 31, 30, 1, 0, 3, 2, 5, 4, 7, 6, 9, 8, 11, 10, 13, 12, 15, 14, 49, 48, 51, 50, 53, 52, 55, 54, 57, 56, 59, 58, 61, 60, 63, 62, 33, 32, 35, 34, 37, 36, 39, 38, 41, 40, 43, 42, 45, 44, 47, 46, 81, 80, 83, 82, 85, 84, 87, 86, 89, 88, 91, 90, 93, 92, 95, 94, 65, 64, 67, 66, 69, 68, 71, 70, 73, 72, 75, 74, 77, 76, 79, 78, 113, 112, 115, 114, 117, 116, 119, 118, 121, 120, 123, 122, 125, 124, 127, 126, 97, 96, 99, 98, 101, 100, 103, 102, 105, 104, 107, 106, 109, 108, 111, 110, 145, 144, 147, 146, 149, 148, 151, 150, 153, 152, 155, 154, 157, 156, 159, 158, 129, 128, 131, 130, 133, 132, 135, 134, 137, 136, 139, 138, 141, 140, 143, 142, 177, 176, 179, 178, 181, 180, 183, 182, 185, 184, 187, 186, 189, 188, 191, 190, 161, 160, 163, 162, 165, 164, 167, 166, 169, 168, 171, 170, 173, 172, 175, 174, 209, 208, 211, 210, 213, 212, 215, 214, 217, 216, 219, 218, 221, 220, 223, 222, 193, 192, 195, 194, 197, 196, 199, 198, 201, 200, 203, 202, 205, 204, 207, 206, 241, 240, 243, 242, 245, 244, 247, 246, 249, 248, 251, 250, 253, 252, 255, 254, 225, 224, 227, 226, 229, 228, 231, 230, 233, 232, 235, 234, 237, 236, 239, 238]

    words = [hashlib.sha256(word).digest()]
    
    for i in range(7):
        words.append(hashlib.sha256(words[i]).digest())
        
    words = b"".join(words)

    for idx in range(0, len(words), 2):
        a = words[idx]
        b = words[idx + 1]
        old = Sbox[a]
        Sbox[a] = Sbox[b]
        Sbox[b] = old
        
    return Sbox

def getbit(byte, i):
    return (byte >> i) & 1

def setbit(v, i):
    return v << i
    
def pbox(byte):
    out = 0
    pos_subs = [4, 1, 0, 6, 3, 5, 7, 2]
    for pos_in in range(8):
        out |= setbit(getbit(byte, pos_in), pos_subs[pos_in])
    return out

def pad1(b):
    while len(b) != 1:
        b = b"\x00" + b
    return b

def r1(i, box):
    out = []

    i = long_to_bytes(i)

    for byte in i:
        out.append(box[byte])

    for idx in range(1, len(out)):
        out[idx] ^= out[idx - 1]

    return  bytes_to_long(b"".join([pad1(long_to_bytes(l)) for l in out]))


def r2(i, box):
    out = []

    i = long_to_bytes(i)

    for byte in i:
        out.append(box[byte])
        
    for idx in range(len(out) - 2, -1, -1):
        out[idx] ^= out[idx + 1]

    return bytes_to_long(b"".join([long_to_bytes(l) for l in out]))

def zpad(i):
    while len(i) != 4:
        i = b"\x00" + i
    return i

def zpad8(i):
    while len(i) < 8:
        i = b"\x00" + i
    return i

def r345(word, k, rnum):
    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum**2 + 20 * rnum**3 - rnum**4) ^ lrot(word, 63 + -43 * rnum + 12 * rnum**2 + -rnum**3)

    word = (4124669716 + word * bytes_to_long(k))**3

    word ^= word << 5
    word ^= word << 5

    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum**2 + 20 * rnum**3 - rnum**4) ^ lrot(word, 63 + -43 * rnum + 12 * rnum**2 + -rnum**3)


    return rrot(word, -504 + 418 * rnum -499 * rnum**2 + -511 * rnum**3 + 98 * rnum**4) & 0xffffffff

def swap(l, r):
    return r, l

def encrypt(i, k, p = False):

    k1 = k[:4]
    k2 = k[4:]

    assert len(k) == 8
    assert len(i) == 8

    m_sbox_1 = get_sbox(k1)
    m_sbox_2 = get_sbox(k2)

    l = bytes_to_long(i[:4])
    r = bytes_to_long(i[4:])
    if (p):
        print("R0:",l, r)
    #round 1
    l ^= r2(r, m_sbox_2) 
    l, r = swap(l,r)
    if (p):
        print("R1:",l, r)
    #round 2
    l ^= r1(r, m_sbox_1)
    l, r = swap(l,r)
    if (p):
        print("R2:",l, r)

    #round 3
    l ^= r345(r, k1, 3)
    l, r = swap(l,r)
    if (p):
        print("R3:",l, r)
    #round 4
    l ^= r345(r, k2, 4)
    l, r = swap(l,r)
    if (p):
        print("R4:",l, r)

    #round 5
    l ^= r345(r, long_to_bytes(bytes_to_long(k2) ^ bytes_to_long(k1)), 5)
    l, r = swap(l,r)
    if (p):
        print("R5:",l, r)

    #round 6
    l ^= r345(r, k1, 6)
    l, r = swap(l,r)
    if (p):
        print("R6:",l, r)

    #round 7
    l ^= r345(r, k2, 7)
    r ^= l
    if (p):
        print("R7:",l, r)

        
    
    return long_to_bytes((l << 32) | r)


# I want you to be happy

# seecrit = b"\x00" + secrets.token_bytes(7)
seecrit = b"\x00" + b"\xde\xad\xbe\xef\x13\x37\xff"

for i in range(1024):
    p = int(input("p: "))
    print(bytes_to_long(encrypt(zpad8(long_to_bytes(p)), seecrit)))

guess = int(input("k: "))
if (guess == bytes_to_long(seecrit)):
    print(open("flag.txt","r").read())
```

Đây là một cipher sử dụng mô hình Feistel để mã hóa. Mô hình Feistel thường xuyên bị tấn công theo phương pháp differential, có thể kể đến như: DES, GOST, hay các phiên bản nhỏ hơn của chúng.

Do đó yêu cầu chống lại differential attack (cũng như người anh em khác của nó là linear attack) trở thành tiêu chuẩn để xây dựng block cipher hiện nay.

#### a. Mô hình Feistel

Trong mô hình Feistel, mỗi block của plaintext sẽ được chia đôi thành hai nửa trái phải - $P = L_0 \Vert R_0$.

Ở bài này, plaintext có $8$ bytes và key cũng có $8$ bytes.

Trong mô hình Feistel chuẩn, ở mỗi vòng $i+1$, sẽ thực hiện biến đổi sau:

$$L_{i+1} = R_i, \quad R_{i+1} = L_i \oplus F(R_i, K_{i+1})$$

Trong đó:

- $K_{i+1}$ là khóa ở vòng $i+1$ với $i = 0, 1, \ldots$
- $F$ được gọi là round function. Hàm $F$ phụ thuộc vào cipher là loại nào. Ví dụ thuật toán DES thì $F$ là các phép biến đổi Expand, P-box và S-box. Hoặc đối với thuật toán GOST thì $F$ gồm cộng modulo $2^{32}$, S-box và dịch $11$ bit sang trái.

Ở mô hình Feistel bên trên (cũng là mô hình chuẩn) thì hàm $F$ cố định cho mỗi vòng. Tuy nhiên ở bài này thì round function ở mỗi vòng khác nhau. Cụ thể thì ở vòng một dùng S-box `r2`, ở vòng thứ hai là S-box `r1`, các vòng sau thì dùng hàm `r345`.

Mình có thể viết quá trình biến đổi như sau:

```{list-table}

* - Vòng $1$
  - $L_1 = R_0$
  - $R_1 = L_0 \oplus r_2(R_0, S_2)$
* - Vòng $2$
  - $L_2 = R_1$
  - $R_2 = L_1 \oplus r_1(R_1, S_1)$
* - Vòng $3$
  - $L_3 = R_2$
  - $R_3 = L_2 \oplus r_{345}(R_2, k_2, 3)$
* - Vòng $4$
  - $L_4 = R_3$
  - $R_4 = L_3 \oplus r_{345}(R_3, k_2, 4)$
* - Vòng $5$
  - $L_5 = R_4$
  - $R_5 = L_4 \oplus r_{345}(R_4, k_1 \oplus k_2, 5)$
* - Vòng $6$
  - $L_6 = R_5$
  - $R_6 = L_5 \oplus r_{345}(R_5, k_1, 6)$
* - Vòng $7$
  - $L_7 = L_6 \oplus r_{345}(R_6, k_2, 7)$
  - $R_7 = R_6 \oplus L_7 = R_6 \oplus r_{345}(R_6, k_2, 7)$
```

Lưu ý rằng vòng cuối hơi khác một tí.

#### b. Differential attack

Differential là gì???

**Định nghĩa.** Xét hàm $S$ từ $\mathbb{F}_2^n$ tới $\mathbb{F}_2^m$. Với mỗi cặp vector $\boldsymbol{a}, \boldsymbol{b} \in \mathbb{F}_2^n$ thì ta nói $\boldsymbol{a} \oplus \boldsymbol{b}$ là **input differential** và $S(\boldsymbol{a}) \oplus S(\boldsymbol{b})$ là **output differential** ứng với hàm $S$.

Hàm $S$ thường là các S-box trong block cipher. Các S-box thường không tuyến tính, nghĩa là ta không có $S(\boldsymbol{a} \oplus \boldsymbol{b}) = S(\boldsymbol{a}) \oplus S(\boldsymbol{b})$.

Differential dựa trên quan sát rằng khi $\boldsymbol{a} \oplus \boldsymbol{b}$ cố định thì output differential $S(\boldsymbol{a}) \oplus S(\boldsymbol{b})$ phân bố không đều. Giả sử mình có S-box như sau:

$$\begin{array}{|c|c|c|c|c|c|c|c|c||c|c|c|c|c|c|c|c|}
    \hline
    x & 0 & 1 & 2 & 3 & 4 & 5 & 6 & 7 & 8 & 9 & 10 & 11 & 12 & 13 & 14 & 15\\ \hline
    S(x) & 3 & 14 & 1 & 10 & 4 & 9 & 5 & 6 & 8 & 11 & 15 & 2 & 13 & 12 & 0 & 7 \\ \hline
\end{array}$$

Nếu mình duyệt qua tất cả cặp $\boldsymbol{a}, \boldsymbol{b} \in \mathbb{F}_2^4$ thì mình sẽ có quan sát sau:

- Nếu input vi sai là $0$ thì output vi sai là $0$ với xác suất $1$.
- Nếu input vi sai là $1$ thì output vi sai là $13$ với xác suất $6 / 16$.
- Nếu input vi sai là $4$ thì output vi sai là $7$ với xác suất $6 / 16$.
- Nếu input vi sai là $8$ thì output vi sai là $5$ với xác suất $6 / 16$.
- Nếu input vi sai là $15$ thì output vi sai là $14$ với xác suất $6 / 16$.

Đây là những output differential với **xác suất cao nhất** ứng với mỗi input differential cố định $\boldsymbol{a} \oplus \boldsymbol{b}$.

Điều đó có nghĩa là cứ trung bình $16$ cặp $\boldsymbol{a} \oplus \boldsymbol{b}$ cho kết quả là $1$ thì có $6$ cặp cho output differential là $13$.

Tận dụng điều này, chúng ta sẽ giải bài tetraethyllead.

Giả sử $(P, C)$ và $(P', C')$ là hai cặp plaintext-ciphertext sao cho khi input differential $P \oplus P'$ cố định thì xác suất xảy ra của output differential $C \oplus C'$ cao nhất. Khi tìm được input và output differential như vậy, ta mã hóa nhiều plaintext khác nhau và khả năng (xác suất) xuất hiện ciphertext tương ứng thỏa mãn differential đó sẽ cao.

Giả sử $P = (L_0, R_0)$ và $P' = (L'_0, R'_0)$ là hai nửa trái phải tương ứng với $P$ và $P'$.

Đặt $\Delta L_{in} = L_0 \oplus L'_0$ và $\Delta R_{in} = R_0 \oplus R_0$ là input differential trước khi mã hóa.

Đặt $\Delta L_{out} = L_7 \oplus L'_7$ và $\Delta_{in} = R_7 \oplus R'_7$ là output differential sau khi mã hóa.

Chúng ta sẽ đi qua từng hàm để xem với input-output differential nào thì khả năng xảy ra là cao nhất.

#### c. Differential vòng 1

Sau vòng $1$ ta có:

- $L_1 = R_0$ và $R_1 = L_0 \oplus r_2(R_0, S_2)$.
- $L'_1 = R'_0$ và $R'_1 = L'_0 \oplus r_2(R'_0, S_2)$.

Khi đó differential ở vòng $1$ là:

- $\Delta L_1 = L_1 \oplus L'_1 = R_0 \oplus R'_0$.
- $\Delta R_1 = R_1 \oplus R'_1 = L_0 \oplus L'_0 \oplus r_2(R_0, S_2) \oplus r_2(R'_0, S_2)$.

Như vậy $\Delta R_1$ phụ thuộc vào vi sai của hàm $r_2$.

```python
def r2(i, box):
    out = []

    i = long_to_bytes(i)

    for byte in i:
        out.append(box[byte])
        
    for idx in range(len(out) - 2, -1, -1):
        out[idx] ^= out[idx + 1]

    return bytes_to_long(b"".join([long_to_bytes(l) for l in out]))
```

Giả sử bốn bytes đầu vào của $r_2$ là $a \Vert b \Vert c \Vert d$. Tiếp theo ta thay thế bốn bytes này bởi giá trị S-box của nó là $S_2(a) \Vert S_2(b) \Vert S_2(c) \Vert S_2(d)$. Vòng lặp thứ hai XOR chồng các bytes lên nhau để có kết quả:

$$S_2(a) \oplus S_2(b) \oplus S_2(c) \oplus S_2(d) \Vert S_2(b) \oplus S_2(c) \oplus S_2(d) \Vert S_2(c) \oplus S_2(d) \Vert S_2(d)$$

Như vậy nếu $R_0 = a \Vert b \Vert c \Vert d$ và $R'_0 = a' \Vert b' \Vert c' \Vert d'$ thì:

$$\begin{align*}
    r_2(R_0, S_2) \oplus r_2(R_0', S_2) = & S_2(a) \oplus S_2(b) \oplus S_2(c) \oplus S_2(d) \oplus S_2(a') \oplus S_2(b') \oplus S_2(c') \oplus S_2(d') \\ 
    \Vert & S_2(b) \oplus S_2(c) \oplus S_2(d') \oplus S_2(b') \oplus S_2(c') \oplus S_2(d') \\ 
    \Vert & S_2(c) \oplus S_2(d) \oplus S_2(c') \oplus S_2(d') \\ 
    \Vert & S_2(d) \oplus S_2(d')
\end{align*}$$

Dễ thấy rằng nếu chúng ta chọn $d = d'$ thì byte cuối triệt tiêu.

Tiếp theo chọn $c = c'$ thì byte kế cuối cũng triệt tiêu.

Tiếp theo chọn $b = b'$ thì byte thứ ba (từ phải sang trái) cũng triệt tiêu.

Khi đó vi sai sẽ là 

$$r_2(R_0, S_2) \oplus r_2(R_0', S_2) = S_2(a) \oplus S_2(a') \Vert 00 \Vert 00 \Vert 00.$$

Bằng một cách *ảo ma* nào đó thì output differential $S_2(a) \oplus S_2(a') = 0x80$ có xác suất xảy ra cao nhất khi input differential là $0x80$. Cái này writeup nói nhưng chúng ta cũng có thể kiểm tra phân bố vi sai của $r_2$.

Đi ngược lên trên thì $a \Vert b \Vert c \Vert d \oplus a' \Vert b' \Vert c' \Vert d' = 80 \Vert 00 \Vert 00 \Vert 00$. Đây chính là vi sai cho $R_0 \oplus R_0'$.

Như vậy $\Delta L_1 = 0x80000000$ (với xác suất là $1$) và $\Delta R_1 = L_0 \oplus L_0' \oplus 0x80000000$ (với xác suất cao).

#### d. Differential vòng 2

Tương tự, đối với $r_1$ chúng ta cũng dùng phương pháp tương tự.

Sau vòng $2$ ta có:

- $L_2 = R_1$ và $R_2 = L_1 \oplus r_1(R_1, S_1)$.
- $L'_2 = R'_1$ và $R'_2 = L'_1 \oplus r_1(R'_1, S_1)$.

Khi đó differential ở vòng $2$ là:

- $$\Delta L_2 = L_2 \oplus L'_2 = R_1 \oplus R'_1 = L_0 \oplus L_0' \oplus 0x80000000$$
 
(với xác suất cao).

- $$\Delta R_2 = R_2 \oplus R'_2 = L_1 \oplus L'_1 \oplus r_1(R_1, S_1) \oplus r_1(R'_1, S_1) = 0x80000000 \oplus r_1(R_1, S_1) \oplus r_1(R'_1, S_1).$$

Khi này, $R_1 \oplus R_1'$ rất khó kiểm soát nên chúng ta sẽ khiến $R_1 = R_1'$. Khi đó $r_1(R_1, S_1) \oplus r_1(R_1', S_1) = 00$ với xác suất bằng $1$.

Nếu $R_1 = R_1'$ thì quay ngược lên trên, $\Delta R_1 = 00 = L_0 \oplus L_0' \oplus 0x80000000$ nên $L_0 \oplus L_0' = 0x80000000$.

Như vậy mình đã tìm được input differential cho cả hàm mã hóa là $L_0 \oplus L_0' = 0x80000000$ và $R_0 \oplus R_0' = 0x80000000$.

Lúc này, differential ở vòng $2$ có xác suất xảy ra cao nhất là $L_2 \oplus L_2' = 0x00000000$ và $R_2 \oplus R_2' = 0x80000000$.

Tiếp theo, mình cần biết output differential nào của toàn bộ hàm `encrypt` sẽ có khả năng xảy ra nhất đối với input differential này.

#### e. Hàm `z345`

```python
def r345(word, k, rnum):
    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum**2 + 20 * rnum**3 - rnum**4) ^ lrot(word, 63 + -43 * rnum + 12 * rnum**2 + -rnum**3)

    word = (4124669716 + word * bytes_to_long(k))**3

    word ^= word << 5
    word ^= word << 5

    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum**2 + 20 * rnum**3 - rnum**4) ^ lrot(word, 63 + -43 * rnum + 12 * rnum**2 + -rnum**3)

    return rrot(word, -504 + 418 * rnum -499 * rnum**2 + -511 * rnum**3 + 98 * rnum**4) & 0xffffffff
```

Khi thay các giá trị `rnum` vào thì mình thấy có $3$ vòng `rrot` và `lrot` ngược nhau (`rrot(word, 17)` và `lrot(word, 15)` trên $32$ bit) nên ở những vòng này `rrot` và `lrot` sẽ triệt tiêu nhau do đa thức.

Tiếp theo, `word ^= word << 5` sẽ không làm thay đổi differential $0x80$. Lấy ví dụ với $8$ bit $\bar{a} = a_0 a_1 a_2 a_3 a_4 a_5 a_6 a_7$ và $\bar{b} = b_0 b_1 b_2 b_3 b_4 b_5 b_6 b_7$. Giả sử $\bar{a} \oplus \bar{b} = 0x80$ thì:

$$\begin{align*}
    \bar{a} \oplus (\bar{a} << 5) \oplus \bar{b} \oplus (\bar{b} << 5) = & a_0 a_1 a_2 a_3 a_4 a_5 a_6 a_7 \oplus a_5 a_6 a_7 0 0 0 0 0 \\ \oplus & b_0 b_1 b_2 b_3 b_4 b_5 b_6 b_7 \oplus b_5 b_6 b_7 00000 \\ = & \underbrace{(a_0 a_1 a_2 a_3 a_4 a_5 a_6 a_7 \oplus b_0 b_1 b_2 b_3 b_4 b_5 b_6 b_7)}_{0x80} \\ \oplus & \underbrace{(a_5 a_6 a_7 00000 \oplus b_5 b_6 b_7 00000)}_{0x00} = 0x80
\end{align*}$$

Cuối cùng, phép nhân modulo $2^{32}$ có $50%$ duy trì differential $0x80000000$ và do đó differential này vẫn có xác suất cao cho cả `z345`.

#### f. Giải

Chiến thuật để giải bài này là:

- Gửi lên các cặp plaintext sao cho $\Delta L_{in} = 0x80000000$ và $\Delta R_{in} = 0x80000000$.
- Nhận các cặp ciphertext tương ứng thỏa mãn $\Delta L_{out} \oplus R_{out} = 0x80000000$.

Các cặp plaintext, ciphertext như trên sẽ giúp ta khôi phục lại khóa.

**Note.** Để thuận tiện thì mình sẽ cố định khóa trong `server.py` và chỉ cần tìm ra khóa là xong. Ở trong giải thì sau khi request đủ $1024$ lần encrypt server cũng không đặt timeout nên chúng ta có thể để script chạy bao lâu tùy ý.

File `solve.py` sau đây tương tác với `server.py` để lấy về các cặp plaintext, ciphertext thỏa mãn điều kiện trên.

```python
import hashlib
from Crypto.Util.number import bytes_to_long, long_to_bytes

def rrot(word, i):
    i %= 32
    word = word & ((1 << 32) - 1)
    return ((word >> i) | (word << (32 - i))) & ((1 << 32) - 1)

def lrot(word, i):
    i %= 32
    word = word & ((1 << 32) - 1)
    return ((word << i) | (word >> (32 - i))) & ((1 << 32) - 1)
    

def get_sbox(word):
    
    Sbox = [17, 16, 19, 18, 21, 20, 23, 22, 25, 24, 27, 26, 29, 28, 31, 30, 1, 0, 3, 2, 5, 4, 7, 6, 9, 8, 11, 10, 13, 12, 15, 14, 49, 48, 51, 50, 53, 52, 55, 54, 57, 56, 59, 58, 61, 60, 63, 62, 33, 32, 35, 34, 37, 36, 39, 38, 41, 40, 43, 42, 45, 44, 47, 46, 81, 80, 83, 82, 85, 84, 87, 86, 89, 88, 91, 90, 93, 92, 95, 94, 65, 64, 67, 66, 69, 68, 71, 70, 73, 72, 75, 74, 77, 76, 79, 78, 113, 112, 115, 114, 117, 116, 119, 118, 121, 120, 123, 122, 125, 124, 127, 126, 97, 96, 99, 98, 101, 100, 103, 102, 105, 104, 107, 106, 109, 108, 111, 110, 145, 144, 147, 146, 149, 148, 151, 150, 153, 152, 155, 154, 157, 156, 159, 158, 129, 128, 131, 130, 133, 132, 135, 134, 137, 136, 139, 138, 141, 140, 143, 142, 177, 176, 179, 178, 181, 180, 183, 182, 185, 184, 187, 186, 189, 188, 191, 190, 161, 160, 163, 162, 165, 164, 167, 166, 169, 168, 171, 170, 173, 172, 175, 174, 209, 208, 211, 210, 213, 212, 215, 214, 217, 216, 219, 218, 221, 220, 223, 222, 193, 192, 195, 194, 197, 196, 199, 198, 201, 200, 203, 202, 205, 204, 207, 206, 241, 240, 243, 242, 245, 244, 247, 246, 249, 248, 251, 250, 253, 252, 255, 254, 225, 224, 227, 226, 229, 228, 231, 230, 233, 232, 235, 234, 237, 236, 239, 238]

    words = [hashlib.sha256(word).digest()]
    print("S-box")
    print(words[0].hex())
    
    for i in range(7):
        words.append(hashlib.sha256(words[i]).digest())
        print(words[-1].hex())
        
    words = b"".join(words)

    for idx in range(0, len(words), 2):
        a = words[idx]
        b = words[idx + 1]
        old = Sbox[a]
        Sbox[a] = Sbox[b]
        Sbox[b] = old

    print()
        
    return Sbox

def getbit(byte, i):
    return (byte >> i) & 1

def setbit(v, i):
    return v << i
    
def pbox(byte):
    out = 0
    pos_subs = [4, 1, 0, 6, 3, 5, 7, 2]
    for pos_in in range(8):
        out |= setbit(getbit(byte, pos_in), pos_subs[pos_in])
    return out

def pad1(b):
    while len(b) != 1:
        b = b"\x00" + b
    return b

def r1(i, box):
    out = []

    i = long_to_bytes(i)

    for byte in i:
        out.append(box[byte])
    print([hex(o) for o in out])

    for idx in range(1, len(out)):
        out[idx] ^= out[idx - 1]
    print([hex(o) for o in out])

    return  bytes_to_long(b"".join([pad1(long_to_bytes(l)) for l in out]))


def r2(i, box):
    out = []

    i = long_to_bytes(i)

    for byte in i:
        out.append(box[byte])
        
    for idx in range(len(out) - 2, -1, -1):
        out[idx] ^= out[idx + 1]

    return bytes_to_long(b"".join([long_to_bytes(l) for l in out]))

def zpad(i):
    while len(i) != 4:
        i = b"\x00" + i
    return i

def zpad8(i):
    while len(i) < 8:
        i = b"\x00" + i
    return i

def r345(word, k, rnum):
    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum**2 + 20 * rnum**3 - rnum**4) ^ lrot(word, 63 + -43 * rnum + 12 * rnum**2 + -rnum**3)

    word = (4124669716 + word * bytes_to_long(k))**3

    word ^= word << 5
    word ^= word << 5

    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum**2 + 20 * rnum**3 - rnum**4) ^ lrot(word, 63 + -43 * rnum + 12 * rnum**2 + -rnum**3)


    return rrot(word, -504 + 418 * rnum -499 * rnum**2 + -511 * rnum**3 + 98 * rnum**4) & 0xffffffff

def swap(l, r):
    return r, l

def encrypt(i, k, p = False):

    k1 = k[:4]
    k2 = k[4:]

    assert len(k) == 8
    assert len(i) == 8

    m_sbox_1 = get_sbox(k1)
    m_sbox_2 = get_sbox(k2)

    LS, RS = [], []

    l = bytes_to_long(i[:4])
    r = bytes_to_long(i[4:])
    if (p):
        # print("R0:", l,  r)
        print(f"R0:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)
    
    #round 1
    l ^= r2(r, m_sbox_2) 
    l, r = swap(l,r)
    if (p):
        # print("R1:",l, r)
        print(f"R1:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)
    
    #round 2
    l ^= r1(r, m_sbox_1)
    l, r = swap(l,r)
    if (p):
        # print("R2:",l, r)
        print(f"R2:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)

    #round 3
    l ^= r345(r, k1, 3)
    l, r = swap(l,r)
    if (p):
        # print("R3:",l, r)
        print(f"R3:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)
    
    #round 4
    l ^= r345(r, k2, 4)
    l, r = swap(l,r)
    if (p):
        # print("R4:",l, r)
        print(f"R4:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)

    #round 5
    l ^= r345(r, long_to_bytes(bytes_to_long(k2) ^ bytes_to_long(k1)), 5)
    l, r = swap(l,r)
    if (p):
        # print("R5:",l, r)
        print(f"R5:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)

    #round 6
    l ^= r345(r, k1, 6)
    l, r = swap(l,r)
    if (p):
        # print("R6:",l, r)
        print(f"R6:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)

    #round 7
    l ^= r345(r, k2, 7)
    r ^= l
    if (p):
        # print("R7:",l, r)
        print(f"R7:\t{l:08x},\t{r:08x}")
        LS.append(l)
        RS.append(r)

    return long_to_bytes((l << 32) | r), LS, RS

import os
import random
from pwn import process, context

# context.log_level = 'Debug'

pr = process(["python3", "server.py"])

pts = []
ct0s = []
ct1s = []

for _ in range(1024 // 2):
    p = random.randrange(0, 2**64)
    pr.sendlineafter(b"p: ", str(p).encode())
    c = int(pr.recvline().strip().decode())
    p_ = 0x8000000080000000 ^ p
    pr.sendlineafter(b"p: ", str(p_).encode())
    c_ = int(pr.recvline().strip().decode())
    lout = (c >> 32) ^ (c_ >> 32)
    rout = (c & 0xffffffff) ^ (c_ & 0xffffffff)
    if (lout ^ rout) == 0x80000000:
        pts.append(p)
        ct0s.append(c)
        ct1s.append(c_)

print(pts)
print(ct0s)
print(ct1s)
```

Sau đó sử dụng thư viện SHA256 từ project [này](https://github.com/System-Glitch/SHA256) (gồm file `SHA256.h` và `SHA256.cpp`).

```C++
#include <iostream>
#include <inttypes.h>
#include <vector>
#include <omp.h>
#include <string.h>
#include <stdlib.h>

#include "SHA256.h"

uint32_t bytes_to_u32(uint8_t* in)
{
    uint32_t result = 0;
    for (int i = 0; i < 4; i++)
        result |= (in[i] << (24 - 8 * i));
    return result;
}

void u32_to_bytes(uint32_t in, uint8_t* out)
{
    for (int i = 0; i < 4; i++)
        out[i] = (in >> (24 - 8 * i)) & 0xff;
}

void u64_to_bytes(uint64_t in, uint8_t* out)
{
    for (int i = 0; i < 8; i++)
        out[i] = (in >> (56 - 8 * i)) & 0xff;
}

uint32_t rrot(uint32_t word, uint32_t i)
{
    i %= 32;
    word = word & 0xffffffff;
    return ((word >> i) | (word << (32 - i))) & 0xffffffff;
}

void get_sbox(uint8_t* word, uint8_t* target)
{
    uint8_t Sbox[] = { 17, 16, 19, 18, 21, 20, 23, 22, 25, 24, 27, 26, 29, 28, 31, 30, 1, 0, 3, 2, 5, 4, 7, 6, 9, 8, 11, 10, 13, 12, 15, 14, 49, 48, 51, 50, 53, 52, 55, 54, 57, 56, 59, 58, 61, 60, 63, 62, 33, 32, 35, 34, 37, 36, 39, 38, 41, 40, 43, 42, 45, 44, 47, 46, 81, 80, 83, 82, 85, 84, 87, 86, 89, 88, 91, 90, 93, 92, 95, 94, 65, 64, 67, 66, 69, 68, 71, 70, 73, 72, 75, 74, 77, 76, 79, 78, 113, 112, 115, 114, 117, 116, 119, 118, 121, 120, 123, 122, 125, 124, 127, 126, 97, 96, 99, 98, 101, 100, 103, 102, 105, 104, 107, 106, 109, 108, 111, 110, 145, 144, 147, 146, 149, 148, 151, 150, 153, 152, 155, 154, 157, 156, 159, 158, 129, 128, 131, 130, 133, 132, 135, 134, 137, 136, 139, 138, 141, 140, 143, 142, 177, 176, 179, 178, 181, 180, 183, 182, 185, 184, 187, 186, 189, 188, 191, 190, 161, 160, 163, 162, 165, 164, 167, 166, 169, 168, 171, 170, 173, 172, 175, 174, 209, 208, 211, 210, 213, 212, 215, 214, 217, 216, 219, 218, 221, 220, 223, 222, 193, 192, 195, 194, 197, 196, 199, 198, 201, 200, 203, 202, 205, 204, 207, 206, 241, 240, 243, 242, 245, 244, 247, 246, 249, 248, 251, 250, 253, 252, 255, 254, 225, 224, 227, 226, 229, 228, 231, 230, 233, 232, 235, 234, 237, 236, 239, 238 };
    uint8_t result[256];

    SHA256 sha256;
    sha256.update(word, 4);
    auto words = sha256.digest();
    memcpy(result, &words[0], 32);

    for (int i = 0; i < 7; i++)
    {
        SHA256 sha;
        sha.update(result + 32 * i, 32);
        auto words = sha.digest();
        memcpy(result + 32 * (i + 1), &words[0], 32);
    }

    for (int i = 0; i < 256; i += 2)
    {
        uint8_t a = result[i];
        uint8_t b = result[i + 1];
        uint8_t old = Sbox[a];
        Sbox[a] = Sbox[b];
        Sbox[b] = old;
    }

    memcpy(target, Sbox, 256);
}

uint32_t lrot(uint32_t word, uint32_t i)
{
    i %= 32;
    word = word & 0xffffffff;
    return ((word << i) | (word >> (32 - i))) & 0xffffffff;
}

uint32_t r1(uint32_t in, const uint8_t* box)
{
    uint8_t s[4] = { 0 };
    u32_to_bytes(in, s);
    for (int i = 0; i < 4; i++)
        s[i] = box[s[i]];

    for (int i = 1; i < 4; i++)
        s[i] ^= s[i-1];

    return bytes_to_u32(s);
}

uint32_t r2(uint32_t in, const uint8_t* box)
{
    uint8_t s[4] = { };
    u32_to_bytes(in, s);
    for (int i = 0; i < 4; i++)
        s[i] = box[s[i]];

    for (int i = 2; i >= 0; i--)
        s[i] ^= s[i+1];

    return bytes_to_u32(s);
}

uint32_t r345(uint32_t word, uint32_t k, uint32_t rnum)
{
    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum * rnum + 20 * rnum * rnum * rnum - rnum * rnum * rnum * rnum) ^ lrot(word, 63 + -43 * rnum + 12 * rnum * rnum + -rnum * rnum * rnum);

    word = (4124669716 + word * k);
    word = word * word * word;

    word ^= word << 5;
    word ^= word << 5;

    word ^= rrot(word, -463 + 439 * rnum + -144 * rnum * rnum + 20 * rnum * rnum * rnum - rnum * rnum * rnum * rnum) ^ lrot(word, 63 + -43 * rnum + 12 * rnum * rnum + -rnum * rnum * rnum);


    return rrot(word, -504 + 418 * rnum -499 * rnum * rnum + -511 * rnum * rnum * rnum + 98 * rnum * rnum * rnum * rnum) & 0xffffffff;
}

uint8_t sbox1[256] = { };
uint8_t sbox2[256] = { };

uint64_t encrypt(uint64_t p, uint64_t key)
{
    uint32_t k1 = key >> 32;
    uint32_t k2 = key & 0xffffffff;

    uint8_t t1[4];
    u32_to_bytes(k1, t1);

    get_sbox(t1, sbox1);

    uint32_t l = p >> 32;
    uint32_t r = p & 0xffffffff;

    // Round 1
    l ^= r2(r, sbox2);
    std::swap(l, r);

    // Round 2
    l ^= r1(r, sbox1);
    std::swap(l, r);

    // Round 3
    l ^= r345(r, k1, 3);
    std::swap(l ,r);

    // Round 4
    l ^= r345(r, k2, 4);
    std::swap(l, r);

    // Round 5
    l ^= r345(r, k1 ^ k2, 5);
    std::swap(l, r);

    // Round 6
    l ^= r345(r, k1, 6);
    std::swap(l, r);

    // Round 7
    l ^= r345(r, k2, 7);
    r ^= l;

    return ((uint64_t)l << 32) | (uint64_t)r;
}

bool test_function()
{
    uint8_t sbox[256] = { 166, 167, 220, 18, 21, 171, 88, 124, 101, 25, 27, 130, 12, 15, 212, 14, 1, 233, 3, 160, 5, 4, 26, 53, 9, 8, 245, 10, 91, 29, 248, 223, 253, 64, 51, 50, 6, 52, 221, 54, 72, 114, 96, 103, 135, 60, 63, 74, 161, 32, 116, 0, 77, 36, 39, 163, 41, 40, 43, 42, 222, 211, 47, 46, 168, 80, 83, 177, 229, 84, 121, 86, 228, 56, 31, 16, 93, 92, 139, 94, 76, 152, 67, 66, 58, 68, 71, 97, 156, 57, 107, 62, 90, 65, 102, 247, 113, 34, 13, 22, 117, 244, 119, 118, 87, 11, 123, 122, 125, 179, 127, 48, 82, 59, 99, 70, 45, 100, 38, 201, 95, 178, 112, 106, 78, 242, 111, 110, 108, 144, 147, 146, 149, 148, 249, 105, 153, 172, 155, 154, 150, 131, 234, 143, 129, 225, 85, 7, 28, 35, 73, 49, 210, 136, 30, 191, 141, 140, 158, 142, 199, 176, 104, 209, 170, 137, 183, 182, 185, 184, 238, 186, 189, 188, 126, 230, 134, 2, 69, 255, 181, 195, 37, 162, 169, 81, 20, 165, 173, 190, 175, 174, 164, 208, 213, 17, 252, 193, 215, 214, 194, 216, 219, 89, 55, 218, 115, 128, 157, 192, 204, 44, 197, 196, 227, 198, 79, 200, 203, 202, 180, 23, 207, 206, 241, 240, 243, 145, 120, 75, 109, 187, 33, 133, 251, 250, 151, 246, 24, 254, 217, 98, 224, 226, 61, 19, 231, 138, 132, 232, 235, 159, 237, 236, 239, 205 };

    if (r1(211416476, sbox) != 210016026) return false;
    if (r2(1111418300, sbox) != 2596923053) return false;
    if (rrot(2386637329, 13) != 2425123337) return false;
    if (lrot(171861653, 13) != 3436355911) return false;
    if (r345(2332062217, 0xdeadbeef, 5) != 3992978025) return false;
    return true;
}

bool check_k2(uint64_t ct0, uint64_t ct1, uint32_t k)
{
    uint32_t L7 = ct0 >> 32;
    uint32_t R7 = ct0 & 0xffffffff;
    uint32_t R6 = R7 ^ L7;
    uint32_t L6 = R7 ^ r345(R6, k, 7);

    uint32_t L7_ = ct1 >> 32;
    uint32_t R7_ = ct1 & 0xffffffff;
    uint32_t R6_ = R7_ ^ L7_;
    uint32_t L6_ = R7_ ^ r345(R6_, k, 7);

    if ((L6 ^ L6_) == 0x80000000)
    {
        return true;
    }
    return false;
}

std::vector<uint32_t> bruteforce_k2()
{
    uint64_t pts[] = { 2194090266659289430ULL, 15801510715588955136ULL, 195752496155878917ULL };
    uint64_t ct0s[] = { 5313144679078469543ULL, 1721352893315118722ULL, 6831354680889557863ULL };
    uint64_t ct1s[] = { 14587251420890060969ULL, 17919522859960426701ULL, 5659069971483530659ULL };


    std::vector<uint32_t> key2 = { };
    
    #pragma omp for
    for (uint64_t k = 0; k < 0x100000000; k++)
    {
        if (check_k2(ct0s[0], ct1s[0], (uint32_t)k))
        {
            if (check_k2(ct0s[1], ct1s[1], (uint32_t)k))
            {
                if (check_k2(ct0s[2], ct1s[2], (uint32_t)k))
                {
                    key2.push_back(k);
                }
            }
        }
    }

    return key2;
}
```

Đầu tiên chúng ta sẽ khôi phục `k2` đi ngược từ ciphertex lên. Chúng ta nhận các khóa thỏa mãn $\Delta L_6 \oplus \Delta R_6 = 0x80000000$ (vòng $6$). Để tìm `k2` thì hàm `main` sẽ là:

```cpp
int main()
{    
    std::vector<uint32_t> key2 = bruteforce_k2();
    for (int i = 0; i < key2.size(); i++)
        std::cout << std::hex << key2[i] << std::endl;
    return 0;
}
```

Sau đó với mỗi `k2` chúng ta bruteforce các `k1` và kiểm tra `k = k1 || k2` nào sẽ encrypt đúng. Ở đây do mình đã cố định khóa ở `server.py` nên mình biết `k2` nào là đúng để tiết kiệm thời gian viết lại writeup. Sau đó thì chỉ cần bruteforce `k1` thôi.

```cpp
int main()
{
    uint8_t k2[] = { 0xef, 0x13, 0x37, 0xff };
    get_sbox(k2, sbox2);
    
    uint64_t p = 2194090266659289430ULL;
    uint64_t c = 5313144679078469543ULL;

    #pragma omp for
    for (uint64_t k1 = 0; k1 < 0xffffff; k1++)
    {
        uint64_t key = (k1 << 32) | 0xef1337ff;
        if (encrypt(p, key) == c)
        {
            std::cout << "Found key: " << std::hex << key << std::endl;
        }
    }
    return 0;
}
```

Cám ơn các bạn đã đọc writeup dài lê thê của mình :)))