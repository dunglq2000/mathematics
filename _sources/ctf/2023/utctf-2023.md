## UTCTF 2023

### Affinity

Đề cho mình 2 source code: `aes.py` và `encrypt_pub.py*`.

Trong bài này có điểm khác thường so với thuật toán AES gốc là **SBOX tuyến tính**. Điều đó có nghĩa là với 2 cặp plaintext-ciphertext bất kì $(P_0, C_0)$ và $(P_i, C_i)$ thì có một ma trận $A$ thỏa $P_0 \oplus P_i = A \cdot (C_0 \oplus C_i)$.

Lưu ý là mỗi block AES có $16$ byte tương đương $128$ bit, nên $A$ là ma trận $128 \times 128$ trên $\mathrm{GF}(2)$. Như vậy mình chọn $P_0 = 0^{128}$, và $P_i = (0, \cdots, 1, \cdots 0)$ với $1$ nằm ở vị trí $i$ ($i = 1, \cdots, 128$). Với đủ $128$ cặp như vậy mình khôi phục được ma trận $A$ từ đó suy ra flag với $P_t = P_0 \oplus A \cdot (C_0 \oplus C_t)$.

### Provably Insecure

Ở bài này Alice cho chúng ta public key RSA $(n, e)$, và cặp $(s, m)$ với $s = m^d \pmod n$.

Nhiệm vụ là tìm các số $(n', e', d')$ sao cho với mỗi số random $x$ thì các điều kiện sau thỏa mãn:

* $n' \neq n$ và $e' \neq e$;
* $n' > s$;
* $x^{e' d'} = 1 \pmod{n'}$;
* $e' > 1$;
* $s^{e'} = m \pmod{n'}$.

Quan trọng là ở điều kiện cuối, ở hai modulo khác nhau nhưng cho cùng kết quả khi decrypt.

Cách làm của mình là, nếu $s^{e'} = m \pmod{n'}$ thì tương đương với $(m^{d'})^{e'} = m \pmod{n'}$. Như vậy mình chọn modulo $n'$ và tính discrete log $m^{d'} = s \pmod{n'}$ và có $d'$. Sau đó mình tìm nghịch đảo $e'$ của $d'$ trong $\varphi(n')$.

Cách làm này cần 2 điều kiện:

* tồn tại discrete log $m^{d'}=s$ trong modulo $n'$;
* $\gcd(d', \varphi(n')) = 1$ để tìm $e'$.

Mình cứ request tới khi có $(s, m)$ thỏa mãn thôi. Với cách làm này thì không cần quan tâm $(n, e)$.

### Looks Wrong tom E

Bài này có $10$ round, mỗi round sẽ sinh một số lượng ma trận trong $\mathrm{GF}(10^9+7)$ (tối đa $10$ ma trận mỗi round).

Với mỗi ma trận, server tạo random vector $s$ và error nhỏ $e$, rồi tính $s \cdot A + e$ và gửi ma trận $A$ lẫn vector $s \cdot A + e$ cho mình.

Nhiệm vụ của mình là chọn ma trận trong số $10$ ma trận đó (hoặc ít hơn), và gửi lên vector $s'$ sao cho tích $s \cdot A$ là vector nhỏ. Cụ thể là $b = s \cdot A = (b_1, b_2, \cdots)$ thì $b_i < 4w$ hoặc $\mathrm{mod} - b_i < 4 w$.

Sau nhiều nỗ lực nghĩ LLL thì mình phát hiện rằng mình cứ gửi $s = (0, 0, \cdots)$ thì kết quả luôn là vector $0$ :))))

Bài cuối mình không thấy sự liên quan hay gì từ đề nên ngậm ngùi chịu chết.

Cám ơn mọi người đã đọc writeup của mình.

Đề và bài giải ở [đây](https://github.com/dunglq2000/CTF/tree/master/2023/UTCTF).
