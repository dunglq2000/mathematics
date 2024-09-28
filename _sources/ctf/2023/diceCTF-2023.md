## Dice CTF 2023

### Provably Secure 1/2

```python
# server.py
#!/usr/local/bin/python

# Normally you have unlimited encryption and decryption query requests in the IND-CCA2 game.
# For performance reasons, my definition of unlimited is 8 lol

from cryptography.hazmat.primitives.asymmetric import rsa, padding
from cryptography.hazmat.primitives import hashes
from secrets import randbits
from os import urandom
from Crypto.Util.strxor import strxor

def encrypt(pk0, pk1, msg):
    r = urandom(16)
    r_prime = strxor(r, msg)
    ct0 = pk0.encrypt(r, padding.OAEP(mgf=padding.MGF1(algorithm=hashes.SHA256()),
                         algorithm=hashes.SHA256(), label=None))
    ct1 = pk1.encrypt(r_prime, padding.OAEP(mgf=padding.MGF1(algorithm=hashes.SHA256()), 
                         algorithm=hashes.SHA256(), label=None))
    return ct0.hex() + ct1.hex()


def decrypt(key0, key1, ct):
    ct0 = ct[:256]
    ct1 = ct[256:]
    r0 = key0.decrypt(ct0, padding.OAEP(mgf=padding.MGF1(algorithm=hashes.SHA256()),
                           algorithm=hashes.SHA256(), label=None))
    r1 = key1.decrypt(ct1, padding.OAEP(mgf=padding.MGF1(algorithm=hashes.SHA256()),
                           algorithm=hashes.SHA256(), label=None))
    return strxor(r0, r1)


if __name__ == '__main__':
    print("""Actions:
0) Solve
1) Query Encryption
2) Query Decryption
""")
    for experiment in range(1, 129):
        print("Experiment {}/128".format(experiment))
        key0 = rsa.generate_private_key(public_exponent=65537, key_size=2048)
        key1 = rsa.generate_private_key(public_exponent=65537, key_size=2048)
        pk0 = key0.public_key()
        pk1 = key1.public_key()
        print("pk0 =", pk0.public_numbers().n)
        print("pk1 =", pk1.public_numbers().n)
        m_bit = randbits(1)
        seen_ct = set()
        en_count = 0
        de_count = 0
        
        while True:
            choice = int(input("Action: "))
            if choice == 0:
                guess = int(input("m_bit guess: "))
                if (guess == m_bit):
                    print("Correct!")
                    break
                else:
                    print("Wrong!")
                    exit(0)
            elif choice == 1:
                en_count += 1
                if (en_count > 8):
                    print("You've run out of encryptions!")
                    exit(0)
                m0 = bytes.fromhex(input("m0 (16 byte hexstring): ").strip())
                m1 = bytes.fromhex(input("m1 (16 byte hexstring): ").strip())
                if len(m0) != 16 or len(m1) != 16:
                    print("Must be 16 bytes!")
                    exit(0)
                msg = m0 if m_bit == 0 else m1
                ct = encrypt(pk0, pk1, msg)
                seen_ct.add(ct)
                print(ct)
            
            elif choice == 2:
                de_count += 1
                if (de_count > 8):
                    print("You've run out of decryptions!")
                    exit(0)
                in_ct = bytes.fromhex(input("ct (512 byte hexstring): ").strip())
                if len(in_ct) != 512:
                    print("Must be 512 bytes!")
                    exit(0)
                if in_ct in seen_ct:
                    print("Cannot query decryption on seen ciphertext!")
                    exit(0)
                print(decrypt(key0, key1, in_ct).hex())

    with open('flag.txt', 'r') as f:
        print("Flag: " + f.read().strip())
```

Chúng ta có 3 lựa chọn (cho đường đời) như sau:

* `Solve`: chỉ ra $m_{bit}$ là $0$ hay $1$, nếu đúng thì vượt $1$ ải, vượt thành công $128$ ải thì qua môn!!!;
* `Query Encryption`: ở mỗi round server tạo hai key RSA để mình dùng. Mình cần nhập hai message có độ dài $16$ byte và gửi lên server. Dựa vào bit random $m_{bit}$ mà server sẽ encrypt $m_0$ hay $m_1$. Server trả về ciphertext tương ứng (hai ciphertext với tổng độ dài $512$ byte);
* `Query Decryption`: để decrypt mình cần gửi lên server ciphertext $512$ byte và chỉ được decrypt mỗi ciphertext một lần.

**NOTE**: mình chỉ được encrypt và decrypt $8$ lần mỗi loại.

Hàm encrypt làm việc như sau:

* lấy tham số là hai public key $pk_0$ và $pk_1$, và plaintext $msg$ $16$ có byte;
* random 1 chuỗi $r$ có $16$ byte;
* tính $r\_ prime = r \oplus msg$;
* tính $ct_0 = \text{ENC}(r, pk_0)$ và $ct_1 = \text{ENC}(r\_prime, pk_1)$;
* cả hai ciphertext đều dùng padding là OAEP và hash là SHA256 nên độ dài là $256$ byte. Hàm trả về ghép hai chuỗi ciphertext lại ($512$ byte).

Hàm decrypt làm ngược lại và ở kết quả cuối thì xor hai plaintext lại ($msg = r\_prime \oplus r$).

Đề chỉ cho hai public key, mình thì thích private key hơn :))))

Mình nhận ra một điều, giả sử ciphertext của mình là $\text{ENC}(r, pk_0)$ và $\text{ENC}(r\_prime = r \oplus msg, pk_1)$ thì nếu mình gửi hai lần decrypt với các ciphertext:

* $\text{ENC}(r, pk_0)$ và $\text{ENC}(00^{16}, pk_1)$ thì kết quả trả về là $r \oplus 00^{16} = r$;
* $\text{ENC}(00^{16}, pk_0)$ và $\text{ENC}(r\_prime = r \oplus msg, pk_1)$ thì kết quả trả về là $00^{16} \oplus r \oplus msg = r \oplus msg$.

Khi đó mình xor hai plaintext này lại là được $msg$ và so sánh xem nó trùng với $m_0$ hay $m_1$ mình gửi lên server ban đầu.

```python
from pwn import remote, process, context
from cryptography.hazmat.primitives.asymmetric import rsa, padding
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.serialization import load_pem_public_key
from Crypto.PublicKey import RSA
from Crypto.Util.strxor import strxor
from tqdm import tqdm

context.log_level = 'Debug'
r = remote("mc.ax", 31497)

# r = process(["python3", "server.py"])

for _ in range(4):
    r.recvline()

p0 = "0" * 32
p1 = "f" * 32

for _ in tqdm(range(128)):
    r.recvline()
    r.recvline()
    pk0 = int(r.recvline().strip().decode().split(" ")[-1])
    pk1 = int(r.recvline().strip().decode().split(" ")[-1])

    key0, key1 = RSA.construct((pk0, 65537)), RSA.construct((pk1, 65537))
    key0_, key1_ = key0.export_key('PEM'), key1.export_key('PEM')

    pk0_ = load_pem_public_key(key0_)
    pk1_ = load_pem_public_key(key1_)

    ct0_ = pk0_.encrypt(bytes(16), padding.OAEP(mgf=padding.MGF1(algorithm=hashes.SHA256()),
                            algorithm=hashes.SHA256(), label=None))
    ct1_ = pk1_.encrypt(bytes(16), padding.OAEP(mgf=padding.MGF1(algorithm=hashes.SHA256()),
                            algorithm=hashes.SHA256(), label=None))

    r.sendlineafter(b"Action: ", b"1")
    r.sendlineafter(b"m0 (16 byte hexstring): ", p0)
    r.sendlineafter(b"m1 (16 byte hexstring): ", p1)

    ct = r.recvline().strip()
    ct0, ct1 = ct[:512], ct[512:]

    payload0 = ct0 + ct1_.hex().encode()

    r.sendlineafter(b"Action: ", b"2")
    r.sendlineafter(b"ct (512 byte hexstring): ", payload0)

    ran = bytes.fromhex(r.recvline().strip().decode())

    payload1 = ct0_.hex().encode() + ct1

    r.sendlineafter(b"Action: ", b"2")
    r.sendlineafter(b"ct (512 byte hexstring): ", payload1)

    ran_m = bytes.fromhex(r.recvline().strip().decode())

    m = strxor(ran, ran_m)

    m_bit = 0
    if m == bytes(16):
        m_bit = 0
    else:
        m_bit = 1

    r.sendlineafter(b"Action: ", b"0")
    r.sendlineafter(b"m_bit guess: ", str(m_bit))

r.recvline()
r.recvline()

r.close()
```

**NOTE**: thật ra ở bài 1 không có công đoạn kiểm tra ciphertext không nằm trong ciphertext có sẵn nên mình chỉ cần gửi lên ciphertext vừa được encrypt là ra. Code trên được dùng để giải cả hai bài Provably Secure 1/2.

Flag **Provably Secure**: `dice{yeah_I_lost_like_10_points_on_that_proof_lmao}`

Flag **Provably Secure 2**: `dice{my_professor_would_not_be_proud_of_me}`

### BBBB

```python
#!/usr/local/bin/python
from Crypto.Util.number import bytes_to_long, getPrime
from random import randint
from math import gcd
from os import urandom

def generate_key(rng, seed):
    e = rng(seed)
    while True:
        for _ in range(randint(10,100)):
            e = rng(e)
        p = getPrime(1024)
        q = getPrime(1024)
        phi = (p-1)*(q-1)
        if gcd(e, phi) == 1:
            break

    n = p*q
    return (n, e)


def generate_params():
    p = getPrime(1024)
    b = randint(0, p-1)

    return (p,b)


def main():
    p,b = generate_params()
    print("[+] The parameters of RNG:")
    print(f"{b=}")
    print(f"{p=}")
    a = int(input("[+] Inject b[a]ckdoor!!: "))
    rng = lambda x: (a*x + b) % p

    keys = []
    seeds = []
    for i in range(5):
        seed = int(input("[+] Please input seed: "))
        seed %= p
        if seed in seeds:
            print("[!] Same seeds are not allowed!!")
            exit()
        seeds.append(seed)
        n, e = generate_key(rng, seed)
        if e <= 10:
            print("[!] `e` is so small!!")
            exit()

        keys.append((n,e))

    FLAG = open("flag.txt", "rb").read()
    assert len(FLAG) < 50
    FLAG = FLAG + urandom(4)

    for n,e in keys:
        r = urandom(16)
        flag = bytes_to_long(FLAG + r)
        c = pow(flag, e, n)
        r = r.hex()
        print("[+] Public Key:")
        print(f"{n=}")
        print(f"{e=}")
        print(f"{r=}")
        print("[+] Cipher Text:", c)


if __name__ == "__main__":
    main()
```

Bài này khoai thật sự :))))

Bài này giống một phần bài [BBB](https://ctftime.org/task/23982) của giải SECCON nhưng có chút khác bọt.

Đề cho mình một số nguyên tố $p$ $512$ bit và số $b$ nhỏ hơn $p$. Mình cần nhập số $a$ và từ đó các số mũ $e$ dùng trong RSA sẽ được tạo bởi hàm `rng`.

Dựa trên bài của giải SECCON, chiến thuật làm bài này là cố gắng khiến hàm `rng` tạo nhiều $e=11$ nhất có thể (ở bài này sẽ là $3$ vì rất khó lấy đủ $5$).

Điểm khó của bài này là hàm `rng` tuyến tính, nghĩa là với mỗi output chỉ tìm được đúng một input. Tuy nhiên chúng ta có thể tìm `rng` sao cho các input tạo thành vòng. Nghĩa là:

$$\begin{align*}
    a X_{i} + b \equiv & X_{i+1} & \pmod p \\
    a X_{i+1} + b \equiv & X_{i+2} & \pmod p \\
    a X_{i+2} + b \equiv & X_{i+3} & \pmod p \\
    a X_{i+3} + b \equiv & X_{i+4} & \pmod p \\
    a X_{i+4} + b \equiv & X_{i} & \pmod p
\end{align*}$$

Ở đây $X_{i} = X_{i+5}$, tức là sau $5$ lần thì các giá trị $X_i$ lặp lại và mình sẽ tìm $a$ thỏa mãn đống này.

Trừ phương trình dưới cho phương trình trên vế theo vế, mình có:

$$\begin{align*}
    a (X_{i+1} - X_i) \equiv & X_{i+2} - X_{i+1} & \pmod p \\
    a (X_{i+2} - X_{i+1}) \equiv & X_{i+3} - X_{i+2} & \pmod p \\
    a (X_{i+3} - X_{i+2}) \equiv & X_{i+4} - X_{i+3} & \pmod p \\
    a (X_{i+4} - X_{i+3}) \equiv & X_{i} - X_{i+4} & \pmod p \\
    a (X_{i} - X_{i+4}) \equiv & X_{i+1} - X_i & \pmod p
\end{align*}$$

Như vậy $a^5 \equiv 1 \pmod p$. Nếu phương trình này có nghiệm khác $1$ thì ta chọn làm tham số $a$.

Tiếp theo, mình cần $e=11$ nằm trong vòng lặp này nên mình cứ chọn $X_0 = e = 11$ rồi theo trình tự $X_{i+1} = a X_i + b \pmod p$ thôi.

Câu hỏi là tại sao lại cần tới $3$ bộ có $e=11$ mà không phải $2$?

Vì với mỗi public key $2048$ bit, phương pháp Coppersmith sẽ hoạt động hiệu quả khi $(2048 * T) \times (1/11 - \varepsilon) \approx 8 \times (L + 4)$ với $L$ là độ dài flag (tối đa là $49$) và $4$ byte random. Như vậy khi $T = 3$ thì $\varepsilon > 0$ là điều mình cần nhắm tới. Tham khảo ở [đây](https://crypto.stackexchange.com/questions/95065/breaking-rsa-with-linear-padding-using-hastads-attack-with-e-11)

Cuối cùng, sử dụng CRT và hastad attack (ví dụ như ở [đây](https://github.com/0n5/CTF-Crypto/blob/master/RSA/hastads.sage)) để giải.

Mình cần lưu ý rằng mình đã biết $5$ byte đầu của flag là `dice{` nên mình có thể giảm độ dài flag cần tìm xuống, từ đó Coppersmith sẽ hiệu quả hơn.

Mỗi phương trình của mình có dạng $(\text{FLAG} \cdot 256^{16} + r_i)^e = c_i \pmod{n_i}$ mà FLAG có $5$ byte đầu là `dice{` nên mình có thể gọi `C = bytes_to_long(b"dice{") << (8 * (L + 4 + 16))`. Phương trình trở thành 

$$(\text{FLAG}' \cdot 256^{16} + C + r_i)^e = c_i \pmod{n_i}$$

```python
from pwn import remote, process, context
from sage.all import *
from Crypto.Util.number import long_to_bytes, bytes_to_long
from tqdm import tqdm

# context.log_level = 'Debug'

rng = lambda a, s, b, p: (a * s + b) % p

def get_a(b, p):
    P = PolynomialRing(Zmod(p), 'x'); x = P.gen()
    e = 11
    f = x**5 - 1
    roots = f.roots()
    for root, _ in roots:
        if root == 1:
            continue
        a = root
        seeds = [e]
        for i in range(4):
            seeds.append(rng(a, seeds[-1], b, p))
        if len(set(seeds)) != len(seeds):
            continue
        assert rng(a, seeds[-1], b, p) == seeds[0]
        return a, seeds
    
    return None, None

def solve(L):
    NUM = len(es)
    e = 11
    a_ = int.from_bytes(b'dice{', 'big') << (8 * (L + 4 + 16))
    for i in range(NUM):
        ns[i] = Integer(ns[i])
        es[i] = Integer(ns[i])
        rs[i] = Integer(rs[i])
        cs[i] = Integer(cs[i])
    TArray = [-1] * NUM
    for i in range(NUM):
        arrayToCRT = [0] * NUM
        arrayToCRT[i] = 1
        TArray[i] = crt(arrayToCRT, ns)
    P = PolynomialRing(Zmod(prod(ns)), 'x'); x = P.gen()
    gArray = [-1] * NUM
    for i in range(NUM):
        gArray[i] = TArray[i] * (pow(256**16 * x + a_ + rs[i], 11) - cs[i])
    g = sum(gArray)
    g = g.monic()
    beta = e * 8 * (L + 4) / (2048 * NUM)
    epsilon = 1 / 32
    roots = g.small_roots(X=2**(8*(L + 4)), beta=beta, epsilon=epsilon)
    # roots = g.small_roots(X=2**(8*(L + 4)), epsilon=(1/11)-(8*(L+4)/(2048*NUM)))
    if len(roots) == 0:
        print("No solutions found!")
        return -1
    for root in roots:
        print(root)
        print(long_to_bytes(int(root)))

rr = process(["python3", "bbbb.py"])
rr.recvline()
b = int(rr.recvline().strip().decode()[2:])
p = int(rr.recvline().strip().decode()[2:])
ns, es, rs, cs = [], [], [], []

a, seeds = get_a(b, p)
if not a:
    print("a not found!")
    exit()

rr.sendlineafter(b"[+] Inject b[a]ckdoor!!: ", str(a).encode())
for seed in seeds:
    rr.sendlineafter(b"[+] Please input seed: ", str(seed).encode())

for _ in range(5):
    rr.recvline()
    n = int(rr.recvline().strip().decode()[2:])
    e = int(rr.recvline().strip().decode()[2:])
    r = int(rr.recvline().strip().decode()[3:-1], 16)
    c = int(rr.recvline().strip().decode().split(" ")[-1])
    if e == 11:
        ns.append(n)
        es.append(e)
        rs.append(r)
        cs.append(c)

assert len(es) >= 3
for L in reversed(range(30, 50)):
    root = solve(L)
    if root != -1:
        m = long_to_bytes(root)
        print(m)
```

**NOTE**: việc chọn beta và epsilon khá khó nhằn, công thức trong code là từ writeup người giải ra :)))) Và không phải lúc nào cũng có $a$ thỏa cũng như đủ 3 bộ có $e=11$. Nên là .......... hên xui :))))
