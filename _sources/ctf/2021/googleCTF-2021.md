## Google CTF 2021

### Pythia

```python
#!/usr/bin/python -u
import random
import string
import time

from base64 import b64encode, b64decode
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.ciphers.aead import AESGCM
from cryptography.hazmat.primitives.kdf.scrypt import Scrypt

max_queries = 150
query_delay = 10

passwords = [bytes(''.join(random.choice(string.ascii_lowercase) for _ in range(3)), 'UTF-8') for _ in range(3)]
flag = open("flag.txt", "rb").read()

print(passwords)

def menu():
    print("What you wanna do?")
    print("1- Set key")
    print("2- Read flag")
    print("3- Decrypt text")
    print("4- Exit")
    try:
        return int(input(">>> "))
    except:
        return -1

print("Welcome!\n")

key_used = 0

for query in range(max_queries):
    option = menu()

    if option == 1:
        print("Which key you want to use [0-2]?")
        try:
            i = int(input(">>> "))
        except:
            i = -1
        if i >= 0 and i <= 2:
          key_used = i
        else:
          print("Please select a valid key.")
    elif option == 2:
        print("Password?")
        passwd = bytes(input(">>> "), 'UTF-8')

        print("Checking...")
        # Prevent bruteforce attacks...
        time.sleep(query_delay)
        if passwd == (passwords[0] + passwords[1] + passwords[2]):
            print("ACCESS GRANTED: " + flag.decode('UTF-8'))
        else:
            print("ACCESS DENIED!")
    elif option == 3:
        print("Send your ciphertext ")
        print(b64encode(passwords[key_used]).decode())

        ct = input(">>> ")
        print("Decrypting...")
        # Prevent bruteforce attacks...
        time.sleep(query_delay)
        try:
            nonce, ciphertext = ct.split(",")
            nonce = b64decode(nonce)
            ciphertext = b64decode(ciphertext)
        except:
            print("ERROR: Ciphertext has invalid format. Must be of the form \"nonce,ciphertext\", where nonce and ciphertext are base64 strings.")
            continue

        kdf = Scrypt(salt=b'', length=16, n=2**4, r=8, p=1, backend=default_backend())
        key = kdf.derive(passwords[key_used])
        try:
            cipher = AESGCM(key)
            plaintext = cipher.decrypt(nonce, ciphertext, associated_data=None)
        except:
            #print(nonce.hex())
            print("ERROR: Decryption failed. Key was not correct.")
            continue

        print("Decryption successful")
    elif option == 4:
        print("Bye!")
        break
    else:
        print("Invalid option!")
    print("You have " + str(max_queries - query) + " trials left...\n")
```

Bài này random ba password từ các ký tự in thường, mỗi password có độ dài là $3$.

Nhiệm vụ của chúng ta là tìm ba password này và ghép lại (theo thứ tự) để lấy flag.

Trong $150$ queries, mình có thể làm một trong ba công việc:

* chọn password được dùng để decrypt;
* test password để lấy flag;
* gửi nonce và ciphertext để kiểm tra xem có thể decrypt bằng AES-GCM không.

Mình sẽ cần hiểu về AES-GCM hoạt động như nào.

#### 1. Counter mode (CTR)

Mình nên bắt đầu với CTR mode trước. Ở đây một bộ đếm (counter) được sử dụng. Chúng ta có thể dùng bộ đếm cơ bản $0, 1, 2, \ldots$ hoặc các bộ đếm phức tạp hơn. Mô hình mã hóa với khóa $K$ là $C_i = P_i \oplus \text{AES}_K (\text{counter}_i)$ hoặc $C_i = E_K (P_i, \text{counter}_i)$ nên việc dùng bộ đếm nào cũng không quá quan trọng, qua hàm $\text{AES}$ thì đều khó cả.

![CTR](../assets/CTR_encryption.png)

#### 2. Authenticated encryption (AEAD)

Một vấn đề quan trọng đối với mã hóa đối xứng (stream cipher và block cipher) là làm sao để kiểm tra thông tin có bị sửa đổi không? Nói cách khác, làm sao phòng ngừa MITM attack?

Khi đó chúng ta thêm 1 trường dữ liệu gọi là _associated data_. Do đó mô hình mã hóa được gọi là _authenticated encryption with associated data_ (AEAD). Chúng ta cần định nghĩa sau:

**Định nghĩa 1**. _Message authentication code_ (MAC) là một hàm bất kì, kí hiệu là $\text{MAC}_K (N, C, A^d)$. Sử dụng secret key $K$ trao đổi bởi Alice và Bob, hàm lấy nonce $N$, ciphertext $C$ và associated data $A^d$ nào đó để tạo ra tag $T$. Dựa vào tag $T$ này Bob kiểm tra tính hợp lệ của ciphertext $C$.

Mình có thể hiểu nonce là một số bất kì thỏa một số tiêu chí về độ dài là được.

Ví dụ, giả sử Alice muốn gửi cho Bob plaintext $P$. Alice chọn nonce $N$ và encrypt plaintext với $C = E_K (N, P)$. Sau đó Alice tạo tag $T = \text{MAC}_K (N, C, A^d)$ và gửi message $M = \{N, C, T\}$ tới cho Bob.

Giả sử Bob nhận được message $M' = \{N', C', T'\}$ và tính $\tau = \text{MAC}_K (N', C', A^d)$ và so sánh với $T'$. Nếu $\tau = T'$ thì ciphertext không bị sai lệch, từ đó Bob decrypt $P'=D_K(N', C')$.

#### 3. Galois/Counter mode (GCM)

![GCM](../assets/GCM_encryption.png)

Ở mode này, phần trên là CTR mode, ở phần dưới có tính toán thêm về associated data để tạo ra tag. Tất cả việc tính toán qua hàm $\text{mult}_H$ hay $C_i \oplus \text{mult}_H$ được thực hiện trên $GF(2^{128})$ (đa thức tối giản là $f(x) = x^{128} + x^7 + x^2 + x + 1$). Lý do của việc này là mỗi block của AES gồm $16$ byte, tương đương $128$ bit, khi đó cần thực hiện chuyển đổi từ block $16$ byte thành đa thức thuộc $GF(2^{128})$.

Giả sử mình có ciphertext $C$ gồm $n$ block. Mình ký hiệu $C = C_0 \Vert C_1 \Vert C_2 \Vert \cdots \Vert C_{n-1}$.

Đối với bài CTF trên thì associated data không dùng nên mình sẽ bỏ qua.

Vậy $H$ trong chỗ $\text{mult}_H$ là gì? Thật ra chỉ là $H = \text{AES}_K (0^{128})$ (128 bit `0`).

* Với lần $\text{mult}_H$ đầu, do không có associated data nên là $0^{128}$;
* Với lần thứ hai, $(0^{128} \oplus C_0) \cdot H = C_0 H$;
* Với lần thứ ba, $(C_0 H \oplus C_1) \cdot H = C_0 H^2 \oplus C_1 H$;
* Cứ tiếp tục như vậy nhưng để ý hai lần $\text{mult}_H$ cuối cùng.
* Trong $128$ bit thì $64$ bit đầu được dùng để chỉ độ dài associated data (không có nên $len(A) = 0$), còn $64$ bit sau dùng để chỉ độ dài ciphertext (theo bit). Do đó ở đây sẽ là $0^{64} \Vert (128 \cdot n)$ (có $n$ block, mỗi block $128$ bit).
* Với lần kế cuối, $C_0 H^{n+1} \oplus C_1 H^{n} \oplus \cdots \oplus L H$ với $L = 0^{64} \Vert (128 \cdot n)$.
* Với lần cuối ta cộng thêm encrypt của $\text{counter}_0$ nữa là xong.

Vậy kết quả cuối cùng của toàn bộ quá trình là tag

$$T = C_0 H^{n+1} + C_1 H^{n} + \cdots + C_{n-1} H^2 + LH + \text{AES}_K (J_0)$$

Theo cách chọn nonce của AES-GCM thì nonce có độ dài 12 byte (96 bit) và 

$$J_0 = \text{IV} \Vert 0^{31} \Vert 1$$

trong đó IV là nonce.

#### 4. Quay lại bài toán

Để giải bài này mình cần làm như sau:

* Cố định $IV$ và $T$;
* Mình chia không gian key thành hai nửa trái phải (tìm nhị phân) và kiểm tra xem key (trong bài là password) nằm ở nửa nào cho tới khi không gian key chỉ còn 1.

Tới đây, mục đích của mình là tìm các ciphertext $C_0, C_1, \cdots, C_{n-1}$ sao cho với tất cả key trong một nửa trái đều cho ra cùng một tag. Khi đó nếu mình gửi ciphertext và tag này lên server, nếu server trả về _Decryption successful_ nghĩa là key cần tìm nằm trong nửa trái, nếu fail nghĩa là key nằm ở nửa phải.

Để tìm được các ciphertext như vậy mình sử dụng nội suy Lagrange (Lagrange interpolation).

Mình thấy rằng

$$T = C_0 H^{n+1} + C_1 H^{n} + \cdots + C_{n-1} H^2 + LH + \text{AES}_K (J_0)$$

Tương đương với 

$$C_0 H^{n-1} + C_1 H^{n-2} + \cdots + C_{n-1} = (LH + \text{AES}_K (J_0) + T) \cdot H^{-2}$$

Với mỗi $K_i$ thuộc nửa trái mình có $H_i = \text{AES}_{K_i}(0^{128})$ và $\text{AES}_{K_i} (J_0)$ tương ứng.

Đặt $f(x) = C_0 x^{n-1} + C_1 x^{n-2} + \cdots + C_{n-1}$. Đa thức này thỏa mãn với mọi key $K_i$ thuộc nửa trái thì $f(H_i) = (L H_i + \text{AES}_{K_i}(J_0) + T) \cdot H_i^{-2}$.

Lưu ý rằng để tìm đa thức $f(x)$ bậc $m$ thì cần $m+1$ cặp $(x_i, f(x_i))$. Do đó ở đây ta chọn $n=len(keys)$ với keys chỉ tất cả key của nửa trái.

Từ đó với $n$ key mình sẽ tìm được $f(x)$ (vì $f(x)$ có bậc $n-1$).

Hàm encrypt một block AES. Hàm chuyển đối từ block $16$ byte sang đa thức thuộc $GF(2^{128})$ và ngược lại

```python
def aes_ecb(key, plaintext):
    return AES.new(key, AES.MODE_ECB).encrypt(plaintext)

def byte_to_pol(block):
    n = int.from_bytes(block, 'big')
    nn = list(map(int, bin(n)[2:].zfill(128)))
    pol = sum(j*x**i for i, j in enumerate(nn))
    return F(pol)

def pol_to_byte(element):
    coeff = element.polynomial().coefficients(sparse=False)
    coeff = coeff + [0] * (128 - len(coeff))
    num = int(''.join(list(map(str, coeff))), 2)
    return int.to_bytes(num, 16, 'big')
```

Hàm attack tìm ciphertext với danh sách key, nonce và tag

```python
def find_poly(keys, nonce, tag):
    points = []
    L = byte_to_pol(b'\x00' * 8 + int.to_bytes(128 * len(keys), 8, 'big'))
    T = byte_to_pol(tag)
    N = nonce + b'\x00' * 3 + b'\x01'

    for key in keys:
        Hi = byte_to_pol(aes_ecb(key, bytes(16)))
        Bi = byte_to_pol(aes_ecb(key, N))
        fHi = ((L * Hi) + Bi + T) * Hi**(-2)
        points.append((Hi, fHi))

    lagrange = R.lagrange_polynomial(points)

    coeff = lagrange.coefficients(sparse=False)[::-1]

    C = b"".join([pol_to_byte(c) for c in coeff])

    return C
```

**LƯU Ý 1**. Do không gian key ban đầu khá lớn ($26^3$) nên việc tìm nhị phân ngay từ đầu khá là khoai (đa thức bậc $26^3 / 2 = 8788$) nên mình chia ra các chunk key dài $512$ để tìm chunk nào chứa key (bản chất không thay đổi). Sau đó từ mỗi chunk mình mới dùng tìm nhị phân mò key.

**LƯU Ý 2**. Việc tính toán đa thức bậc $512$ cũng tốn thời gian nên chúng ta có thể tính trước rồi lưu lại trên dict hoặc hash table hoặc bất cứ thứ gì bạn nghĩ ra :v sau đó chúng ta mới giao tiếp với server.

Phần còn lại của code là attack thôi :))))

```python
from pwn import remote, process, context
from sage.all import *
from Crypto.Cipher import AES
from itertools import product
import string
from base64 import b64encode, b64decode
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.ciphers.aead import AESGCM
from cryptography.hazmat.primitives.kdf.scrypt import Scrypt
from tqdm import tqdm
import os

# context.log_level = 'Debug'

F2 = GF(2)['x']
x = F2.gen()
modulus = x**128 + x**7 + x**2 + x + 1
F = GF(2**128, 'x', modulus=modulus)
R = PolynomialRing(F, 'z')
z = R.gen()

NONCE = b'\x00' * 12
TAG = b'\x00' * 16

possible_keys = {}
keys = []
for a, b, c in product(string.ascii_lowercase, repeat=3):
    kdf = Scrypt(salt=b'', length=16, n=2**4, r=8, p=1, backend=default_backend())
    password = bytes(a+b+c, 'UTF-8')
    key = kdf.derive(password)
    possible_keys[key] = password
    keys.append(key)

p = process(["python3", "service.py"])

CACHE = {}
chunk_size = 512
for i in tqdm(range(0, len(keys), chunk_size)):
    test_keys = [key for key in keys[i:i+chunk_size]]
    C = find_poly(test_keys, NONCE, TAG)
    CACHE[i] = C
    aes = AES.new(test_keys[0], AES.MODE_GCM, nonce=NONCE)
    aes.decrypt_and_verify(C, TAG)

def attack(idx):
    p.sendlineafter(b">>> ", b"1")
    p.sendlineafter(b">>> ", str(idx).encode())
    # phase 1
    index = 0
    for cache in CACHE:
        C = CACHE[cache]
        payload = b64encode(NONCE) + b"," + b64encode(C + TAG)
        p.sendlineafter(b">>> ", b"3")
        p.sendlineafter(b">>> ", payload)
        p.recvline()
        if b'success' in p.recvline():
            index = cache
            break
    print(cache)
    # phase 2
    test_keys = [key for key in keys[cache:cache + chunk_size]]
    while len(test_keys) > 1:
        C = find_poly(test_keys[:len(test_keys) // 2], NONCE, TAG)
        payload = b64encode(NONCE) + b"," + b64encode(C + TAG)
        p.sendlineafter(b">>> ", b"3")
        p.sendlineafter(b">>> ", payload)
        p.recvline()
        if b"success" in p.recvline():
            test_keys = test_keys[:len(test_keys) // 2]
        else:
            test_keys = test_keys[len(test_keys) // 2:]
    return test_keys[0]

password = b""

for _ in range(3):
    password += possible_keys[attack(_)]

p.sendlineafter(b">>> ", b"2")
p.sendlineafter(b">>> ", password)
print(p.recvline())
print(p.recvline())
p.close()
```

Với mỗi password mình dùng một query để chỉ định vị trí password ($0, 1, 2$), $\lceil 26^3 / 512 \rceil = 35$ query cho mỗi chunk, và $\log_2(512) = 9$ cho tìm nhị phân. Như vậy mình tốn $(1 + 35 + 9) \cdot 3 = 135$ query tổng cộng.

Bài viết tới đây là hết. Cám ơn các bạn đã đọc.
