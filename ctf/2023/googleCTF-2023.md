## Google CTF 2023

### LEAST COMMON GENOMINATOR?

```python
from secret import config
from Crypto.PublicKey import RSA
from Crypto.Util.number import bytes_to_long, isPrime

class LCG:
    lcg_m = config.m
    lcg_c = config.c
    lcg_n = config.n

    def __init__(self, lcg_s):
        self.state = lcg_s

    def next(self):
        self.state = (self.state * self.lcg_m + self.lcg_c) % self.lcg_n
        return self.state

if __name__ == '__main__':

    assert 4096 % config.it == 0
    assert config.it == 8
    assert 4096 % config.bits == 0
    assert config.bits == 512

    # Find prime value of specified bits a specified amount of times
    seed = 211286818345627549183608678726370412218029639873054513839005340650674982169404937862395980568550063504804783328450267566224937880641772833325018028629959635
    lcg = LCG(seed)
    primes_arr = []
    
    dump = True
    items = 0
    dump_file = open("dump.txt", "w")

    primes_n = 1
    while True:
        for i in range(config.it):
            while True:
                prime_candidate = lcg.next()
                if dump:
                    dump_file.write(str(prime_candidate) + '\n')
                    items += 1
                    if items == 6:
                        dump = False
                        dump_file.close()
                if not isPrime(prime_candidate):
                    continue
                elif prime_candidate.bit_length() != config.bits:
                    continue
                else:
                    primes_n *= prime_candidate
                    primes_arr.append(prime_candidate)
                    break
        
        # Check bit length
        if primes_n.bit_length() > 4096:
            print("bit length", primes_n.bit_length())
            primes_arr.clear()
            primes_n = 1
            continue
        else:
            break

    # Create public key 'n'
    n = 1
    for j in primes_arr:
        n *= j
    print("[+] Public Key: ", n)
    print("[+] size: ", n.bit_length(), "bits")

    # Calculate totient 'Phi(n)'
    phi = 1
    for k in primes_arr:
        phi *= (k - 1)

    # Calculate private key 'd'
    d = pow(config.e, -1, phi)

    # Generate Flag
    assert config.flag.startswith(b"CTF{")
    assert config.flag.endswith(b"}")
    enc_flag = bytes_to_long(config.flag)
    assert enc_flag < n

    # Encrypt Flag
    _enc = pow(enc_flag, config.e, n)

    with open ("flag.txt", "wb") as flag_file:
        flag_file.write(_enc.to_bytes(n.bit_length(), "little"))

    # Export RSA Key
    rsa = RSA.construct((n, config.e))
    with open ("public.pem", "w") as pub_file:
        pub_file.write(rsa.exportKey().decode())
```

Bài này sinh ra $8$ số nguyên tố để mã hóa. Từ một trạng thái seed ban đầu $s$, số tiếp theo được sinh ra bởi số trước bởi công thức $s_{i+1} = (m s_i + c) \bmod{n}$.

Chúng ta chỉ biết seed ban đầu, không biết $m$, $c$ hay $n$. Đề cho chúng ta dãy $6$ số đầu tạo bởi chuỗi trên, giả sử là $s_0$, $s_1$, $s_2$, ...

Mình thấy rằng $s_1 = (m s_0 + c) \bmod n$, $s_2 = (m s_1 + c) \bmod n$ và $s_3 = (m s_2 + c) \bmod n$.

Trừ vế theo vế mình có $s_2 - s_1 = m (s_1 - s_0) \bmod n$ và $s_3 - s_2 = m (s_2 - s_1) \bmod n$.

Suy ra $n \mid (s_2 - s_1) - m (s_1 - s_0)$ và $n \mid (s_3 - s_2) - m (s_2 - s_1)$. Như vậy nhân chéo lên để khử $m$ mình thu được 

$$\begin{cases}
    n \mid (s_2 - s_1)^2 - m(s_1 - s_0) (s_2 - s_1) \\ 
    n \mid (s_3 - s_2) (s_1 - s_0) - m (s_2 - s_1) (s_1 - s_0)
\end{cases},$$

hay tương đương với 

$$n \mid (s_2 - s_1)^2 - (s_3 - s_2)(s_1 - s_0)$$

Tương tự như vậy với các cặp khác, dùng gcd mình sẽ tìm ra được $n$.

Khi đã có $n$, nhớ lại rằng $s_2 - s_1 = m (s_1 - s_0) \bmod n$ sẽ suy ra được $m$. Cuối cùng do $s_1 = (m s_0 + c) \bmod n$ nên sẽ tìm được $c$.

Có đủ $n$, $m$ và $c$ mình chạy hàm như đề bài là sẽ tìm được các số nguyên tố từ đó decrypt ra được kết quả.

```python
s0 = 2166771675595184069339107365908377157701164485820981409993925279512199123418374034275465590004848135946671454084220731645099286746251308323653144363063385
s1 = 6729272950467625456298454678219613090467254824679318993052294587570153424935267364971827277137521929202783621553421958533761123653824135472378133765236115
s2 = 2230396903302352921484704122705539403201050490164649102182798059926343096511158288867301614648471516723052092761312105117735046752506523136197227936190287
s3 = 4578847787736143756850823407168519112175260092601476810539830792656568747136604250146858111418705054138266193348169239751046779010474924367072989895377792
s4 = 7578332979479086546637469036948482551151240099803812235949997147892871097982293017256475189504447955147399405791875395450814297264039908361472603256921612
s5 = 2550420443270381003007873520763042837493244197616666667768397146110589301602119884836605418664463550865399026934848289084292975494312467018767881691302197
s_ = 211286818345627549183608678726370412218029639873054513839005340650674982169404937862395980568550063504804783328450267566224937880641772833325018028629959635

def gcd(a, b):
    while b:
        a, b = b, a % b
    return a

u = -(s2 - s1)**2 + (s1 - s0)*(s3 - s2)
v = -(s2 - s1)*(s3 - s2) + (s1 - s0)*(s4 - s3)
w = (s3 - s2)**2 - (s2 - s1)*(s4 - s3)

n = gcd(gcd(u, v), w) // 7
m = pow(s1-s2, -1, n) * (s2-s3) % n
c = (s1 - m*s0) % n


class LCG:
    lcg_m = m
    lcg_c = c
    lcg_n = n

    def __init__(self, lcg_s):
        self.state = lcg_s

    def next(self):
        self.state = (self.state * self.lcg_m + self.lcg_c) % self.lcg_n
        return self.state
    
primes_arr = []
primes_n = 1
lcg = LCG(s_)

from Crypto.Util.number import isPrime, bytes_to_long, long_to_bytes
from Crypto.PublicKey import RSA

while True:
    for i in range(8):
        while True:
            prime_candidate = lcg.next()
            if not isPrime(prime_candidate):
                continue
            elif prime_candidate.bit_length() != 512:
                continue
            else:
                primes_n *= prime_candidate
                primes_arr.append(prime_candidate)
                break
    
    if primes_n.bit_length() > 4096:
        primes_arr.clear()
        primes_n = 1
        continue
    else:
        break

print(primes_arr)

n = 1
for j in primes_arr:
    n *= j
print("[+] Public Key: ", n)
print("[+] size: ", n.bit_length(), "bits")

# Calculate totient 'Phi(n)'
phi = 1
for k in primes_arr:
    phi *= (k - 1)

# Calculate private key 'd'
d = pow(65537, -1, phi)
rsa = RSA.importKey(open("public.pem").read())
assert rsa.n == n
assert rsa.e == 65537

with open("flag.txt", "rb") as f:
    data = int.from_bytes(f.read(), "little")
    m = pow(data, d, n)
    print(long_to_bytes(m))

# b'CTF{C0nGr@tz_RiV35t_5h4MiR_nD_Ad13MaN_W0ulD_b_h@pPy}'
```

### Cursved

```python
# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

from hashlib import sha256
from os import urandom

def bytes_to_hexstr(buf):
  return "".join(["{0:02X}".format(b) for b in buf])
def bytes_to_int(buf):
  return int(bytes_to_hexstr(buf), 16)
def random_int(n):
  return bytes_to_int(urandom(n))
def sha256_as_int(x):
  return int(sha256(x).hexdigest(), 16)
def check_type(x, types):
  if len(x) != len(types):
    return False
  for a,b in zip(x, types):
    if not isinstance(a, b):
      return False
  return True

class Curve:
  def __init__(self, p, D, n):
    self.p = p
    self.D = D
    self.n = n
  def __repr__(self):
    return f"Curve(0x{self.p:X}, 0x{self.D:X})"
  def __eq__(self, other):
    return self.p == other.p and self.D == other.D
  def __matmul__(self, other):
    assert(check_type(other, (int, int)))
    assert(other[0]**2 % self.p == (self.D*other[1]**2 + 1) % self.p)
    return Point(self, *other)

class Point:
  def __init__(self, C, x, y):
    assert(isinstance(C, Curve))
    self.C = C
    self.x = x
    self.y = y
  def __repr__(self):
    return f"(0x{self.x:X}, 0x{self.y:X})"
  def __eq__(self, other):
    assert(self.C == other.C)
    return self.x == other.x and self.y == other.y
  def __add__(self, other):
    assert(self.C == other.C)
    x0, y0 = self.x, self.y
    x1, y1 = other.x, other.y
    return Point(self.C, (x0*x1 + self.C.D*y0*y1) % self.C.p, (x0*y1 + x1*y0) % self.C.p)
  def __rmul__(self, n):
    assert(check_type((n,), (int,)))
    P = self.C @ (1, 0)
    Q = self
    while n:
      if n & 1:
        P = P + Q
      Q = Q + Q
      n >>= 1
    return P
  def to_bytes(self):
    l = len(hex(self.C.p)[2:])
    return self.x.to_bytes(l, "big") + self.y.to_bytes(l, "big")

class Pub:
  def __init__(self, G, P):
    self.G = G
    self.P = P
  def verify(self, m, sig):
    assert(check_type(sig, (Point, int)))
    (R, s) = sig
    e = sha256_as_int(R.to_bytes() + self.P.to_bytes() + m) % self.G.C.n
    return s*self.G == R + e*self.P

class Priv:
  def __init__(self, k, G):
    self.k = k
    self.G = G
    self.P = k*G
  def get_pub(self):
    return Pub(self.G, self.P)
  def sign(self, m):
    r = random_int(16) % self.G.C.n
    R = r*self.G
    e = sha256_as_int(R.to_bytes() + self.P.to_bytes() + m) % self.G.C.n
    return (R, (r + self.k*e) % self.G.C.n)

class Problem:
  def __init__(self, pub):
    self.pub = pub
    self.nonce = None
  def gen(self):
    self.nonce = urandom(16)
    return self.nonce
  def parse_response(self, resp):
    try:
      Rx, Ry, s = (int(t) for t in resp.split())
      return (self.pub.P.C @ (Rx, Ry), s)
    except:
      pass
    return None
  def test(self, sig):
    if self.nonce is None:
      return False
    return self.pub.verify(self.nonce, sig)

from config import FLAG, PRIVATE_KEY

def main():
  C = Curve(0x34096DC6CE88B7D7CB09DE1FEC1EDF9B448D4BE9E341A9F6DC696EF4E4E213B3,
            0x3,
            0x34096DC6CE88B7D7CB09DE1FEC1EDF9B448D4BE9E341A9F6DC696EF4E4E213B2)
  G = C @ (0x2, 0x1)
  priv = Priv(PRIVATE_KEY, G)
  pub = priv.get_pub()
  print(f"pub = {pub.P}")

  prob = Problem(pub)
  nonce = prob.gen()
  print(f"nonce = {bytes_to_hexstr(nonce)}")

  resp = input("sig = ")
  sig = prob.parse_response(resp)
  if sig is not None and prob.test(sig):
    print(FLAG)
  else:
    print("Please try again!")

if __name__ == "__main__":
  try:
    main()
  except:
    pass
```

Bài này định nghĩa một đường cong (có lẽ vậy) là tập hợp các điểm thỏa phương trình $x^2 = D y^2 + 1 \bmod p$ với $D = 3$ và $p$ là số nguyên tố cho trước.

Phép cộng hai điểm $(x_1, y_1)$ và $(x_2, y_2)$ được định nghĩa là điểm $(x_1 x_2 + D y_1 y_2, x_1 y_2 + x_2 y_1)$ (tất cả trong modulo $p$).

Đề bài cho chúng ta biết điểm generator là $G = (2, 1)$, public key là một điểm không đổi trong tất cả lần chạy (điểm $P$). Mình gọi $k$ là private key, là một số trong modulo $n = p-1$ sao cho $P = k G$.

Hướng tấn công của bài này là xây dựng một homomorphism từ nhóm các điểm trên lên $\mathrm{GF}(p)$ và giải discrete logarithm trên $\mathrm{GF}(p)$. Mình xét ánh xạ

$$\varphi: \mathbb{F}_p \times \mathbb{F}_p \to \mathbb{F}_p, \quad (x, y) \to x + yW$$

Ở đây $W$ là một số nào đó thuộc $\mathrm{GF}(p)$. Mình muốn ánh xạ này là homomorphism thì tương đương với điều kiện

$$\varphi(x_1, y_1) \cdot \varphi(x_2, y_2) = \varphi(x_1 x_2 + D y_1 y_2, x_1 y_2 + x_2 y_1)$$

Tương đương với

$$(x_1 + y_1 W) \cdot (x_2 + y_2 W) = (x_1 x_2 + D y_1 y_2) + (x_1 y_2 + x_2 y_1) W$$

Khai triển và thu gọn mình có được $W^2 = D$. Như vậy $W = \sqrt{3} \bmod p$.

Và đúng là $D$ là số chính phương modulo $p$ thật, quá tốt :))))

Như vậy mình sẽ chuyển việc tính toán discrete logarithm $P = k G$ trên tập hợp các điểm trên thành việc tính toán discrete logarithm ứng với phương trình

$$(x_G + y_G W)^k = (x_P + y_P W) \bmod p$$

Tới đây thì khá bế tắc vì $p-1$ có các thừa số rất lớn. Mình đi "hỏi thăm" 1 vòng thì biết có tool open source rất mạnh để tính việc này là [cado-nfs](https://github.com/cado-nfs/cado-nfs).

Đặt $g = x_G + y_G W \bmod p$ và $h = x_P + y_P W \bmod p$. Lúc giải mình thấy một điều lạ lùng là mình không dùng tool trên tính dlog modulo 2 được, nên mình chỉ tính dlog của $g$ và $h$ trên modulo $(p-1)/2$. Cado-nfs sẽ trả về base, mình gọi là $b$, và dlog của $g$ và $h$ lần lượt là $t_1$ và $t_2$.

Do $g = b^{t_1}$, $h = b^{t_2}$, $h = g^k$ nên $b^{t_2} = b^{t_1 k}$ (tất cả modulo $p$). Suy ra $t_2 = t_1 k \bmod \dfrac{p-1}{2}$, từ đó mình tìm được $k$ và $k$ này thỏa mãn $P = k G$.

Như vậy mình đã khôi phục lại private key và sẵn sàng ký bất cứ `nonce` nào gửi tới.

```python
from pwn import remote, context, process

context.log_level = 'Debug'

C = Curve(0x34096DC6CE88B7D7CB09DE1FEC1EDF9B448D4BE9E341A9F6DC696EF4E4E213B3,
        0x3,
        0x34096DC6CE88B7D7CB09DE1FEC1EDF9B448D4BE9E341A9F6DC696EF4E4E213B2)
G = C @ (0x2, 0x1)
P = C @ (0x2FE4D1B7BA0F64D6E5BD5E4E8D55E898FF13B76974646D97BFDCD9DC688C0E2F, 0x8C33E2FC2957EFF24DD1CD5382169C3BFAAC2E75A900D322A8C84D3C641A27E)
x = 597042838662739992479017662198571932571177156379622917145185173378909836425
print(x * G == P)
r = remote("cursved.2023.ctfcompetition.com", 1337)
#r = process(["python3", "chal.py"])
priv = Priv(x, G)
r.recvline()
pub = r.recvline().strip().decode().split(" ")
nonce = r.recvline().strip().decode().split(" ")[-1]
print(priv.get_pub().P)
print(nonce)
sig = priv.sign(bytes.fromhex(nonce))
Rx, Ry, s = sig[0].x, sig[0].y, sig[1]
r.sendlineafter(b"sig = ", " ".join(str(i) for i in [Rx, Ry, s]).encode())
r.recvline()
r.close()

# b'CTF{pe11_conics_are_not_quite_e11iptic_curves}\n'
```

### MHK2

```python
import secrets

random = secrets.SystemRandom()

MSG = "CTF{????}"


class PrivateKey:
    def __init__(self, length: int = 256, keytup: tuple = ()):
        if keytup:
            self.s1, self.s2, self.s, self.p1, self.p2, self.e1, self.e2 = keytup
        else:
            while True:
                self.s1 = self._gen_sequence(length)
                self.p1 = sum(self.s1) + 2
                self.e1 = self._gen_pos_ints(self.p1)
                if is_prime(self.p1): break

            while True:
                self.s2 = self._gen_sequence(length)
                self.p2 = sum(self.s2) + 2
                self.e2 = self._gen_pos_ints(self.p2)
                if is_prime(self.p2): break

            self.s = [self.s1[i] + self.s2[i] for i in range(length)]
            assert self.p1 != self.p2

    def _gen_sequence(self, length: int) -> list[int]:
        return [random.getrandbits(128) for _ in range(length)]

    def _gen_pos_ints(self, p) -> int:
        return random.randint((p-1)//2, p-1)

    def export_secret(self):
        return {"s1": self.s1, "s2": self.s2, "s": self.s,
                "p1": self.p1, "p2": self.p2, "e1": self.e1, "e2": self.e2}


class PublicKey:
    def __init__(self, private_key: PrivateKey):
        self.a1 = [(private_key.e1 * s) % private_key.p1 for s in private_key.s1]
        self.a2 = [(private_key.e2 * s) % private_key.p2 for s in private_key.s2]

        self.b1 = [i % 2 for i in private_key.s1]
        self.b2 = [i % 2 for i in private_key.s2]
        self.b = [i % 2 for i in private_key.s]

        self.t = random.randint(1, 2)
        self.c = self.b1 if self.t == 1 else self.b2

    def public_key_export(self):
        return {"a1": self.a1, "a2": self.a2, "b": self.b, "c": self.c}


class MHK2:
    def __init__(
        self,
        length: int,
        private_key: PrivateKey = PrivateKey,
        public_key: PublicKey = PublicKey,
    ):
        self.private_key = private_key(length)
        self.public_key = public_key(self.private_key)

    def _random_bin_sequence(self, n):
        return [random.randint(0, 1) for _ in range(n)]

    def encrypt(self, msg: str):
        ciphertext = []
        msg_int = f'{(int.from_bytes(str.encode(msg), "big")):b}'
        for i in msg_int:
            ciphertext.append(self.encrypt_bit(int(i)))
        return ciphertext

    def decrypt(self, ciphertext):
        plaintext_bin = ""
        for i in ciphertext:
            plaintext_bin += str(self.decrypt_bit(i))

        split_bin = [plaintext_bin[i : i + 7] for i in range(0, len(plaintext_bin), 8)]

        plaintext = ""
        for seq in split_bin:
            plaintext += chr(int(seq, 2))
        return plaintext

    # single bit {0,1}
    def encrypt_bit(self, bit):
        r1 = self._random_bin_sequence(len(self.public_key.b))
        r2 = self._random_bin_sequence(len(self.public_key.b))

        m1 = sum([(self.public_key.b[i] * r1[i]) for i in range(len(r1))]) % 2
        m2 = sum([(self.public_key.b[i] * r2[i]) for i in range(len(r2))]) % 2

        eq = sum([(self.public_key.c[i] * r1[i]) for i in range(len(r1))]) == sum(
            [(self.public_key.c[i] * r2[i]) for i in range(len(r2))]
        )

        while m1 != bit or m2 != bit or not eq or r1 == r2:
            r1 = self._random_bin_sequence(len(self.public_key.b))
            r2 = self._random_bin_sequence(len(self.public_key.b))

            m1 = (
                sum(
                    [
                        (self.public_key.b[i] * r1[i])
                        for i in range(len(self.public_key.b))
                    ]
                )
                % 2
            )
            m2 = (
                sum(
                    [
                        (self.public_key.b[i] * r2[i])
                        for i in range(len(self.public_key.b))
                    ]
                )
                % 2
            )

            eq = sum(
                [(self.public_key.c[i] * r1[i]) for i in range(len(self.public_key.b))]
            ) == sum(
                [(self.public_key.c[i] * r2[i]) for i in range(len(self.public_key.b))]
            )

        C1 = sum([(self.public_key.a1[i] * r1[i]) for i in range(len(r1))])
        C2 = sum([(self.public_key.a2[i] * r2[i]) for i in range(len(r2))])
        return C1, C2

    def decrypt_bit(self, ciphertext: tuple[int, int]) -> int:
        C1, C2 = ciphertext
        M1 = (
            pow(self.private_key.e1, -1, self.private_key.p1) * C1 % self.private_key.p1
        )
        M2 = (
            pow(self.private_key.e2, -1, self.private_key.p2) * C2 % self.private_key.p2
        )
        m = (M1 + M2) % 2
        return m


def main():
    crypto = MHK2(256)
    ciphertext = crypto.encrypt(MSG)
    plaintext = crypto.decrypt(ciphertext)

    print(crypto.public_key.public_key_export())
    print(ciphertext)

    assert plaintext == MSG


if __name__ == "__main__":
    main()
```

Bài này phức tạp :))))

#### 1. Tạo private key

Để tạo private key, server random hai dãy số $s_1 = (s_{11}, s_{12}, \ldots, s_{1n})$ và $s_2 = (s_{21}, s_{22}, \ldots, s_{2n})$ với $n = 256$ và $s_{ij}$ $128$ bit.

Hệ thống sinh dãy số cho tới khi $\displaystyle{p_1 = \sum_{i=1}^n s_{1i} + 2}$ là số nguyên tố, tương tự cho $\displaystyle{p_2 = \sum_{i=1}^n s_{2i} + 2}$ là số nguyên tố. Sau đó hệ thống chọn ngẫu nhiên số $e_1 \in \Bigl[\dfrac{p_1}{2}, p_1\Bigl]$ và $e_2 \in \Bigl[\dfrac{p_2}{2}, p_2\Bigr]$.

Cuối cùng tính 

$$s = (s_{11} + s_{21}, s_{12} + s_{22}, \ldots, s_{1n} + s_{2n}) = (s_1, s_2, \ldots, s_n).$$

#### 2. Tạo public key

Từ hai dãy $s_1$ và $s_2$ ở trên hệ thống tính hai dãy $a_1 = (e_1 * s_{11}, e_1 * s_{12}, \ldots, e_1 * s_{1n})$ (tất cả trong modulo $p_1$) và $a_2 = (e_2 * s_{21}, e_2 * s_{22}, \ldots, e_2 * s_{2n})$ (tất cả trong modulo $p_2$).

Đặt 

$$b_1 = (s_{11} \bmod 2, s_{12} \bmod 2, \ldots, s_{1n} \bmod 2).$$

Đặt 

$$b_2 = (s_{21} \bmod 2, s_{22} \bmod 2, \ldots, s_{2n} \bmod 2).$$

Đặt

$$b = (s_1 \bmod 2, s_2 \bmod 2, \ldots, s_n \bmod 2).$$

Cuối cùng, $c$ được chọn ngẫu nhiên, hoặc là $b_1$, hoặc là $b_2$.

#### 3. Mã hóa

Để mã hóa một bit, $\mathrm{bit} \in \{0, 1\}$, đầu tiên tạo hai dãy ngẫu nhiên $r_1 = (r_{11}, r_{12}, \ldots, r_{1n})$ và $r_2 = (r_{21}, r_{22}, \ldots, r_{2n})$ với $r_{ij} \in \{0, 1\}$.

Khi đó ciphertext là $c_1 = \sum_{i=1}^n a_{1i} \cdot r_{1i}$ và $c_2 \sum_{i=1}^n a_{2i} \cdot r_{2i}$ (điều kiện đối với $\mathrm{bit}$ ở $m_1$, $m_2$ và $eq$ nhưng hiện tại chúng ta không cần dùng tới).

#### 4. Khôi phục private key

Chi tiết cách giải bài này mình tham khảo writeup của Google và Mystiz. Về mặt lý thuyết mình không hiểu sao họ có thể nghĩ ra lattice hay như vậy :)))) Do đó ở đây mình chỉ trình bày cách xây dựng lattice để giải bài này.

Ý tưởng là từ public key $a_1$ ($a_2$ tương tự) mình sẽ khôi phục lại $p_1$ và $e_1$.

Đặt $A_1 = \sum_{i=1}^n a_{1i}$. 

Do $a_{1i} = e_1 \cdot s_{1i} \bmod p_1$ với $i = \overline{1, n}$ nên $A_1 = \sum\limits_{i=1}^n e_1 \cdot s_{1i} = e_1 \sum\limits_{i=1}^N s_{1i}$. Mà mình đã biết $p_1 = \sum\limits_{i=1}^n s_{1i} + 2$ nên phương trình trên tương đương với $A_1 = e_1 * (p_1 - 2)$. Lấy modulo $p_1$ ta có $A_1 \equiv -2 e_1 \bmod p_1$.

Từ việc $a_{1i} \equiv e_1 \cdot s_{1i} \bmod p_1$, ta có $2 a_{1i} \equiv 2 e_1 \cdot s_{1i} \equiv -A_1 \cdot s_{1i} \bmod p_1$.

Nghĩa là tồn tại số $x_{1i} \in \mathbb{Z}$ sao cho $2 a_{1i} + A_1 \cdot s_{1i} = x_{1i} \cdot p_1$ với $i = \overline{1, n}$.

Mình có thể đánh giá $x_{1i}$ đơn giản như sau: 

$$x_{1i} = \dfrac{2 a_{1i} + A_1 s_{1i}}{p_1} \leqslant \dfrac{2 \max(a_{1i}) + A_1 \cdot 2^{128}}{\max(a_{1i})}$$

xấp xỉ 136 bit.

Lấy $i=1$ ta có $2 a_{11} + A_1 \cdot s_{11} = x_{11} \cdot p_1$ (1).

Lấy $2 \leqslant i \leqslant n$ ta có $2 a_{1i} + A_1 \cdot s_{1i} = x_{1i} \cdot p_1$ (2).

Để khử $p_1$ mình nhân hai vế phương trình (1) cho $x_{1i}$ và nhân hai vế phương trình (2) cho $x_{11}$, rồi trừ vế theo vế thu được $2 a_{11} \cdot x_{1i} - 2 a_{1i} \cdot x_{11} + A_1 (s_{11} \cdot x_{1i} - s_{1i} \cdot x_{11}) = 0$.

Ở đây chúng ta đã biết $a_{11}$, $a_{1i}$ và $A_1$. Việc xây dựng lattice sẽ dựa trên các hệ số $x_{1i}$, $x_{11}$ và $s_{11} \cdot x_{1i} - s_{1i} * s_{11}$. Do đó mình viết

$$\begin{array}{ccc}
    x_{11} & \cdot & (\ldots, -2a_{1i}, \ldots) \\ 
    x_{1i} & \cdot & (\ldots, 2a_{11}, \ldots) \\ 
    \ldots & \cdot & (\ldots, \ldots, \ldots) \\ 
    (s_{11} \cdot x_{1i} - s_{1i} * x_{11}) & * & (\ldots, A_1, \ldots) \\ 
    \ldots & \cdot & (\ldots, \ldots, \ldots)
\end{array}$$

Với $i = \overline{2, n}$ thì mình sẽ cần $255$ cột. Tuy nhiên chúng ta thường sử dụng $1$ để khi tính ra lattice thì sẽ thu được số cần tìm, cụ thể ở đây là $x_{11}$ và $s_{11} \cdot x_{1i} - s_{1i} \cdot x_{11}$. Do đó mình sẽ modify nhẹ lại lattice trên thành

$$\begin{array}{ccc}
    x_{11} & \cdot & (1, \ldots, -2a_{1i}, \ldots) \\ 
    x_{1i} & \cdot & (\ldots, \ldots, 2a_{11}, \ldots) \\ 
    \ldots & \cdot & (\ldots, \ldots, \ldots, \ldots) \\ 
    (s_{11} \cdot x_{1i} - s_{1i} * x_{11}) & * & (0, 1, \ldots, A_1, \ldots) \\ 
    \ldots & \cdot & (\ldots, \ldots, \ldots, \ldots)
\end{array}$$

Ở dòng $s_{11} \cdot x_{1i} - s_{1i} \cdot x_{11}$ chúng ta không muốn nó đụng độ với số $x_{11}$ bên trên nên sẽ dịch qua phải một ô. Ta cần $255$ cột như vậy vì sẽ có $i=\overline{2, 256}$. Và để sắp xếp $-2 a_{1i}$ cũng cần $255$ cột như đã nói ở trên. Vậy lattice này có $1 + 255 + 255 = 511$ cột và cũng là số hàng. Lattice như vậy sẽ có dạng ma trận như sau

$$\begin{pmatrix}1 & 0 & 0 & \ldots & -2a_{12} & -2a_{13} & \ldots \\ 0 & 0 & 0 & \ldots & 2a_{11} & 0 & \ldots \\ 0 & 0 & 0 & \ldots & 0 & 2a_{11} & \ldots \\ \ldots & \ldots & \ldots & \ldots & \ldots & \ldots & \ldots \\ 0 & 1 & \ldots & \ldots & A_1 & 0 & \ldots \\ 0 & 0 & 1 & \ldots & 0 & A_1 & \ldots \\ \ldots & \ldots & \ldots & \ldots & \ldots & \ldots & \ldots \\ \end{pmatrix}$$

Tới lúc này chúng ta đã hoàn thành ... 10% chặng đường. Lý do là vì với lattice này chúng ta không thể giải ra short vector mong muốn được. Dựa trên lattice mình hy vọng sẽ chạy ra vector

$$v = (x_{11}, s_{11} \cdot x_{12} - s_{12} \cdot x_{11}, \ldots, s_{11} \cdot x_{1n} - s_{1n} \cdot x_{11}, 0, 0, \ldots, 0)$$

Tuy nhiên cần nhớ rằng $s_{1i}$ có $128$ bit và $x_{1i}$ xấp xỉ $136$ bit. Bằng tính toán có thể thấy $s_{11} \cdot x_{1i} - s_{1i} \cdot x_{11}$ cũng có $128$ bit. Như vậy chúng ta cần scale lattice trên để các giá trị không sai khác nhau quá lớn.

Cụ thể, do $x_{11}$ có $136$ bit nên ta sẽ nhân với $\dfrac{1}{2^{136}}$, do $s_{11} \cdot x_{1i} - s_{1i} \cdot x_{11}$ có $128$ bit nên ta sẽ nhân với $\dfrac{1}{2^{128}}$. Đối với $-2a_{1i}$, $2a_{11}$ và $A_1$ thì mình cần chúng lớn để lattice tìm ra short vector, nên nhân với $2^{1024}$.

Sử dụng tính chất

$$\begin{pmatrix} a_{11} & a_{12} & \ldots & a_{1n} \\ a_{21} & a_{22} & \ldots & a_{2n} \\ \ldots & \ldots & \ldots & \ldots \\ a_{n1} & a_{n2} & \ldots & a_{nn} \end{pmatrix} \times \begin{pmatrix} b_1 & 0 & 0 & 0 \\ 0 & b_2 & 0 & 0 \\ 0 & 0 & \ddots & 0 \\ 0 & 0 & 0 & b_n \end{pmatrix} = \begin{pmatrix} a_{11} b_1 & a_{12} b_2 & \ldots & a_{1n} b_n \\ a_{21} b_1 & a_{22} b_2 & \ldots & a_{2n} b_n \\ \ldots & \ldots & \ldots & \ldots \\ a_{n1} b_1 & a_{n2} b_2 & \ldots & a_{nn} b_n \end{pmatrix}$$

Mình sẽ nhân lattice trên với ma trận sau là sẽ scale được hệ số theo nhu cầu

$$\begin{pmatrix}\dfrac{1}{2^{136}} & & & & & & \\ & \dfrac{1}{2^{128}} & & & & & \\ & & \ddots & \dfrac{1}{2^{128}} & & & & \\ & & & & 2^{1024} & & \\ & & & & & \ddots & \\ & & & & & & 2^{1024}\end{pmatrix}$$

Phần tử đầu tiên của short vector là $x_{11}$ (có lẽ vậy :v). Thật ra thì phần tử đầu tiên của short vector là $x_{11} \bmod a_{11}$ hoặc $-x_{11} \bmod a_{11}$. Phía trên mình đã tính được chặn trên của $x_{11}$ là $\dfrac{2 \max(a_{1i}) + A_1 \cdot 2^{128}}{\max(a_{1i})}$. Từ đây mình duyệt vòng for qua các giá trị $x_{11} + k a_{11}$ và $-x_{11} + k a_{11}$ để tìm các số $s_{1i}$ theo cách sau

##### a. Khôi phục modulo

Nhắc lại $2 a_{11} + A_1 \cdot s_{11} = x_{11} \cdot p_1$. Modulo hai vế cho $A_1$ thì được $2 a_{11} = x_{11} * p_1 \bmod A_1$. Ở đây có thể tìm được $p_1 = 2a_{11} x_{11}^{-1} \bmod A_1$. Tuy nhiên chúng ta cần lưu ý rằng điều kiện để tồn tại nghịch đảo là $\gcd(x_{11}, A_1) = 1$. Do đó để đảm bảo chúng ta tính toán thêm một bước.

Đặt $g = \gcd(2a_{11}, A_1)$. Khi đó phương trình đồng dư có nghiệm khi và chỉ khi $\gcd(x_{11} \cdot p_1, A_1)$ chia hết cho $g$. Sau khi thỏa các điều kiện này, đặt $\dfrac{A_1}{g} = A_1'$, $2 a_{11}' = \dfrac{2a_{11}}{g} \bmod \dfrac{A_1}{g}$, và $x_{11}' = \dfrac{x_{11}}{g} \bmod \dfrac{A_1}{g}$. Khi đó $p_1 = 2a_{11}' \cdot x_{11}'^{-1} \bmod A_1'$.

##### b. Khôi phục e

Bên trên mình đã có $A_1 = -2e_1 \bmod p_1$ nên mình sẽ tìm được $e_1$. Sau đó từ $a_1 = (a_{11}, a_{12}, \ldots, a_{1n})$ và $e_1$ mình tính lại được tất cả $s_{1i}$ và kiểm tra xem $\sum\limits_{i=1}^n s_i + 2 \equiv p_1$, đồng thời không có số $s_{1i}$ nào vượt quá $128$ bit.

##### c. Code giải

Đoạn code mình lấy của Google. Lưu ý rằng sau khi LLL xong mình cần scale ngược lại độ lớn ban đầu, ở đây là chia cho ma trận $Q$. Do một chút lười nên ở đây thay `a2` thành `a_1` để áp dụng cho $p_1$.

```python
M = Matrix(QQ, 511, 511)
sum_a = sum(a2)
M[0, 0] = 1
for i in range(255):
    M[256+i, i+1] = 1

for i in range(255):
    M[0, 256+i] = -2*a2[i+1]
    M[i+1, 256+i] = 2*a2[0]
    M[256+i, 256+i] = sum_a

weights = [1/2^136] + [1/2^128 for _ in range(255)] + [2^1024 for _ in range(255)]
Q = diagonal_matrix(weights)

M *= Q
M = M.LLL()
print(f"Done LLL!")
M /= Q

for row in M:
    x0_ = row[0]
    y = row[1:256]
    zeros = row[256:]

    if list(y) == [0 for _ in range(255)]: continue
    if min(zeros) != 0: continue
    if max(zeros) != 0: continue

    x0_bound = (2*max(a2) + sum_a * 2^128) // max(a2)
    for x0 in range(+x0_, x0_bound, +a2[0]):
        u, v, m = x0, 2*a2[0], sum_a
        #print(u, v, m)
        g = gcd(v, m)
        if gcd(u, m) % g != 0: continue
        u, v, m = u // g, v // g, m // g
        try:
            p1 = int(Zmod(m)(v/u))
            if p1 % 2 == 0: continue
            if not is_prime(p1): continue
            e = int(Zmod(p1)(-sum_a / 2))
            if e == 0 or gcd(e, p1) != 1: continue
            s = [int(Zmod(p1)(a_/e)) for a_ in a2]
            if sum(s) + 2 != p1: continue
            if max(s) >= 2^128: continue
            print(f"Found! p = {p1}, e = {e}")
        except:
            pass

    for x0 in range(-x0_, x0_bound, +a2[0]):
        u, v, m = x0, 2*a2[0], sum_a
        #print(u, v, m)
        g = gcd(v, m)
        if gcd(u, m) % g != 0: continue
        u, v, m = u // g, v // g, m // g
        try:
            p1 = int(Zmod(m)(v/u))
            if p1 % 2 == 0: continue
            if not is_prime(p1): continue
            e = int(Zmod(p1)(-sum_a / 2))
            if e == 0 or gcd(e, p1) != 1: continue
            s = [int(Zmod(p1)(a_/e)) for a_ in a2]
            if sum(s) + 2 != p1: continue
            if max(s) >= 2^128: continue
            print(f"Found! p = {p1}, e = {e}")
        except:
            pass
```

Cuối cùng chạy decrypt và lấy flag thôi.

```python
# CTF{faNNYPAcKs_ARe_4maZiNg_AnD_und3Rr@t3d}
```

### MYTLS

```python
#!/usr/bin/env python3

# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


import binascii
from cryptography import x509
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives import serialization
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives import hmac
from cryptography.hazmat.primitives.asymmetric import ec
from cryptography.hazmat.primitives.asymmetric import padding
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.primitives.kdf.hkdf import HKDF
import hashlib
import os
from secrets import token_hex


with open('/app/flag.txt') as f:
  _FLAG = f.read()
os.unlink('/app/flag.txt')

def print_encrypted(message, iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  encryptor = cipher.encryptor()
  message = message.encode('utf-8')
  payload = encryptor.update(
      message + b'\x00' * (16 - len(message) % 16)) + encryptor.finalize()
  print(binascii.hexlify(payload).decode('utf-8'))


def input_encrypted(iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  decryptor = cipher.decryptor()
  payload = input()
  payload = binascii.unhexlify(payload)
  res = decryptor.update(payload)
  return res.strip(b'\x00')


def main():
  # Getting the CA cert.
  with open('ca-crt.pem', 'rb') as ca_file:
    ca = x509.load_pem_x509_certificate(ca_file.read())
  # Getting the server cert.
  with open('server-ecdhcert.pem', 'rb') as server_cert_file:
    server_cert_content = server_cert_file.read()
    server_cert = x509.load_pem_x509_certificate(server_cert_content)
  print(server_cert_content.decode('utf-8'))
  # Checking the server key, just to be sure.
  ca.public_key().verify(
      server_cert.signature,
      server_cert.tbs_certificate_bytes,
      padding.PKCS1v15(),
      server_cert.signature_hash_algorithm)
  # Getting the server private key.
  with open('server-ecdhkey.pem', 'rb') as server_key_file:
    server_key = serialization.load_pem_private_key(server_key_file.read(),
                                                    None, default_backend())
  # Getting the client cert.
  print('Please provide the client certificate in PEM format:')
  client_cert_content = ''
  client_cert_line = None
  while client_cert_line != '':
    client_cert_line = input()
    client_cert_content += client_cert_line + '\n'
  client_cert = x509.load_pem_x509_certificate(
      client_cert_content.encode('utf-8'))
  # Checking the client key, this is important. We don't want fakes here!
  ca.public_key().verify(
      client_cert.signature,
      client_cert.tbs_certificate_bytes,
      padding.PKCS1v15(),
      client_cert.signature_hash_algorithm)

  # Get ephemeral client random
  print('Please provide the ephemeral client random:')
  client_ephemeral_random = input()
  if len(client_ephemeral_random) != 32:
    print('ERROR: invalid client random length')
    exit(1)

  # Get ephemeral client key
  print('Please provide the ephemeral client key:')
  client_ephemeral_key_content = ''
  client_ephemeral_key_line = None
  while client_ephemeral_key_line != '':
    client_ephemeral_key_line = input()
    client_ephemeral_key_content += client_ephemeral_key_line + '\n'
  client_ephemeral_public_key = serialization.load_pem_public_key(
      client_ephemeral_key_content.encode('utf-8'))

  # Generate ephemeral server random
  server_ephemeral_random = token_hex(16)
  print('Server ephemeral random:')
  print(server_ephemeral_random)

  # Generate ephemeral server key
  server_ephemeral_key = ec.generate_private_key(ec.SECP256R1(),
                                                 default_backend())
  server_ephemeral_public_key = server_ephemeral_key.public_key()
  print('Server ephemeral key:')
  print(server_ephemeral_public_key.public_bytes(
      encoding=serialization.Encoding.PEM,
      format=serialization.PublicFormat.SubjectPublicKeyInfo).decode('utf-8'))

  server_ephemeral_secret = server_ephemeral_key.exchange(
      ec.ECDH(), client_ephemeral_public_key)
  server_secret = server_key.exchange(ec.ECDH(), client_cert.public_key())
  derived_key = HKDF(algorithm=hashes.SHA256(),
                     length=32,
                     salt=b'SaltyMcSaltFace',
                     info=b'mytls').derive(
                         server_ephemeral_secret +
                         server_secret +
                         client_ephemeral_random.encode('utf-8') +
                         server_ephemeral_random.encode('utf-8'))

  print('Please provide the client HMAC:')
  client_hmac_content = input()
  client_hmac = hmac.HMAC(derived_key, hashes.SHA256())
  client_hmac.update(b'client myTLS successful!')
  client_hmac.verify(binascii.unhexlify(client_hmac_content))

  server_hmac = hmac.HMAC(derived_key, hashes.SHA256())
  server_hmac.update(b'server myTLS successful!')
  print('Server HMAC:')
  print(binascii.hexlify(server_hmac.finalize()).decode('utf-8'))

  message = 'Hello guest!'
  if 'CN=admin.mytls' in client_cert.subject.rfc4514_string():
      message = 'Hello admin! ' + _FLAG

  print_encrypted(message, server_ephemeral_random, derived_key)
  while True:
    print_encrypted(
        'Welcome to our write-only file storage!\n\n'
        'Select the storage slot [0-9]:',
        server_ephemeral_random, derived_key)
    storage_slot = input_encrypted(server_ephemeral_random, derived_key)
    path = os.path.join('/tmp/storage/', storage_slot.decode('utf-8'))
    print_encrypted('Gimme your secrets:', server_ephemeral_random,
                    derived_key)
    secret = input_encrypted(server_ephemeral_random, derived_key)
    with open(path, 'rb+') as f:
      h = hashlib.new('sha256')
      h.update(f.read())
      prev_hash = h.hexdigest()
      f.seek(0)
      f.write(secret)
      print_encrypted('Saved! Previous secret reference: ' + prev_hash,
                      server_ephemeral_random, derived_key)

if __name__ == '__main__':
  main()
```

Bài này dựa trên nguyên lý handshake của TLS (mãi sau mình đàm đạo với các bạn khác mới biết :v). Trong bài này đề cho các file sau:

* admin-ecdhcert.pem
* ca-crt.pem
* Dockerfile
* guest-ecdhcert.pem
* guest-ecdhkey.pem
* server-ecdhcert.pem
* server.py
* start.sh

Ở bài này xảy ra hai công đoạn trao đổi khóa, mình sẽ gọi là `share_key` và `share_ephemeral_key`.

Đối với `share_ephemeral_key`, mình sẽ cần gửi lên một chuỗi hex độ dài $32$ ký tự, và một public key ECDH theo dạng PEM. Server cũng sẽ tạo một chuỗi hex độ dài $32$ ký tự, private key và public key ECDH, sau đó gửi public key ECDH này về cho mình cũng ở dạng PEM.

Khi đó `share_ephemeral_key` sẽ được tính là

```python
server_ephemeral_secret = client_ephemeral_private_key.exchange(
    ec.ECDH(), server_ephemeral_public_key)
```

Điều này là tương đương với đoạn code sau của đề vì việc trao đổi khóa sẽ giống nhau ở hai bên trao đổi khóa.

```python
server_ephemeral_secret = server_ephemeral_key.exchange(
      ec.ECDH(), client_ephemeral_public_key)
```

Do đó mình chỉ cần tạo một ECDH key mỗi lần trao đổi khóa, hoặc tạo một lần cũng được.

Tiếp theo là `share_key`.

Ở đầu bài, mình sẽ cần cung cấp một public key (certificate) cho server. Server sẽ sử dụng ca-crt.pem để verify xem cert của mình có hợp lệ không (có được ký bởi CA không). Server cũng sẽ đọc private key tương ứng (ở file `server-ecdhkey.pem`) và tiến hành trao đổi khóa ECDH lần hai.

```python
server_secret = server_key.exchange(ec.ECDH(), client_cert.public_key())
```

Đoạn code trên thực hiện việc thực hiện trao đổi khóa với certificate (public key) nhận từ client, và server private key.

Mình thấy rằng đề đã cung cấp cho mình hai file cert và key của guest đã được ký bởi CA. Do đó mình dùng `guest-ecdhcert.pem` làm `client_cert`, và đề cũng đã cho mình `server-ecdhcert.pem` nên mình có thể tính toán khóa trao đổi ở phía mình.

```python
server_secret = client_key.exchange(ec.ECDH(), server_cert.public_key())
```

Đoạn code sau đây sẽ thực hiện việc bắt tay trên TLS.

```python
r = remote("mytls.2023.ctfcompetition.com", 1337)
r.recvuntil(b'Please provide the client certificate in PEM format:')
with open("guest-ecdhcert.pem", "rb") as f:
    for line in f.readlines():
        r.send(line)
r.sendline()

# Exchange ECDH
r.sendlineafter(b'Please provide the ephemeral client random:', bytes(16).hex().encode())
r.recvuntil(b'Please provide the ephemeral client key:')
with open("client-ecdhcert.pem", "rb") as f:
    for line in f.readlines():
        r.send(line)
r.sendline()

# Get server ephemeral public key
r.recvuntil(b'Server ephemeral random:\n')
server_random = r.recvline().strip()
r.recvuntil(b'Server ephemeral key:\n')

server_cert = b""
while True:
    data = r.recvline()
    if data == b'\n': break
    server_cert += data

server_cert = serialization.load_pem_public_key(server_cert)
# Load client epehmeral private key
with open("client-ecdhkey.pem", "rb") as f:
    client_ephemeral_private_key = serialization.load_pem_private_key(
        f.read(),
        None,
        default_backend()
    )

# Calculate shared key
server_ephemeral_secret = client_ephemeral_private_key.exchange(ec.ECDH(), server_cert)

# Exchange cert and key
with open("server-ecdhcert.pem", "rb") as f:
    #server_public_key = serialization.load_pem_public_key(f.read())
    server_public_key = x509.load_pem_x509_certificate(f.read())
    server_public_key = server_public_key.public_key()
    #print(server_public_key)

with open("guest-ecdhkey.pem", "rb") as f:
    client_key = serialization.load_pem_private_key(f.read(), None)
    
server_secret = client_key.exchange(ec.ECDH(), server_public_key)

derived_key = HKDF(algorithm=hashes.SHA256(),
                length=32,
                salt=b'SaltyMcSaltFace',
                info=b"mytls").derive(
                    server_ephemeral_secret +
                    server_secret +
                    bytes(16).hex().encode() +
                    server_random
                )

#print(server_random)
#print(client_ephemeral_secret, len(client_ephemeral_secret))
#print(server_secret, len(server_secret))
client_hmac = hmac.HMAC(derived_key, hashes.SHA256())
client_hmac.update(b'client myTLS successful!')
r.sendlineafter(b'Please provide the client HMAC:\n', client_hmac.finalize().hex().encode())

server_hmac = hmac.HMAC(derived_key, hashes.SHA256())
server_hmac.update(b'server myTLS successful!')
r.recvuntil(b'Server HMAC:\n')
assert server_hmac.finalize().hex() == r.recvline().strip().decode()
```

Tuy nhiên tới đây chúng ta vấp phải một vấn đề, đó là subject được ký trên certificate phải là `admin.tls`, trong khi nếu sử dụng `guest-ecdhcert.pem` thì subject là `guest.tls`. Hmm tình hình có vẻ khá phức tạp. Tới đây thì mình chịu chết, sau giải mới làm ra :D

Khi nhìn vào file Docker, mình thấy rằng file `server-ecdhkey`.pem cũng được chép vào container. Từ đó, ở mỗi lần chạy vòng lặp, mình sẽ chỉ định path của file thành `../../app/server-ecdhkey.pem` để thoát khỏi path `/tmp/storage`, vì khi đó mình sẽ "đọc" được một ít thông tin nào đó từ `server-ecdhkey.pem`.

Do `server-ecdhcert.pem` có $241$ bytes, mình đoán rằng `server-ecdhkey.pem` cũng có $241$ bytes. Do đó chiến thuật của mình là ghi đè lên $240$ bytes đầu của `server-ecdh.pem`, server sẽ trả về hash `H(240_bytes_ghi_đè || byte_cuối)`. Mình có thể bruteforce byte cuối với $240$ bytes ghi đè ban đầu fix sẵn.

Sau đó mình connect lại. Với byte cuối đã biết, mình sẽ bruteforce byte kế cuối với $239$ bytes ghi đè. Lúc này server trả về hash `H(239_bytes_ghi_đè || byte_kế_cuối || byte_cuối)`.

Như vậy mình bruteforce từ dưới lên với công thức `((240-số bytes đã biết) || byte_cần_brute || bytes_đã_biết)` (có 241 bytes).

Full code để bruteforce `server-ecdhkey.pem`:

```python
from pwn import remote, context
from cryptography.hazmat.primitives import serialization
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.asymmetric import ec
from cryptography.hazmat.primitives.asymmetric import rsa
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.primitives.kdf.hkdf import HKDF
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives import hmac
from cryptography import x509
import binascii
import hashlib

#context.log_level = 'Debug'

def print_encrypted(message, iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  encryptor = cipher.encryptor()
  message = message.encode('utf-8')
  payload = encryptor.update(
      message + b'\x00' * (16 - len(message) % 16)) + encryptor.finalize()
  #print(binascii.hexlify(payload).decode('utf-8'))
  return binascii.hexlify(payload).decode('utf-8')


def print_decrypted(message, iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  decryptor = cipher.decryptor()
  #message = message.encode('utf-8')
  message = bytes.fromhex(message)
  payload = decryptor.update(message)
  return payload.strip(b"\x00")


def input_encrypted(iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  decryptor = cipher.decryptor()
  payload = input()
  payload = binascii.unhexlify(payload)
  res = decryptor.update(payload)
  return res.strip(b'\x00')


key_path = "../../app/server-ecdhkey.pem"
known = ''

while True:
    r = remote("mytls.2023.ctfcompetition.com", 1337)
    r.recvuntil(b'Please provide the client certificate in PEM format:')
    with open("guest-ecdhcert.pem", "rb") as f:
        for line in f.readlines():
            r.send(line)
    r.sendline()

    # Exchange ECDH
    r.sendlineafter(b'Please provide the ephemeral client random:', bytes(16).hex().encode())
    r.recvuntil(b'Please provide the ephemeral client key:')
    with open("client-ecdhcert.pem", "rb") as f:
        for line in f.readlines():
            r.send(line)
    r.sendline()

    # Get server ephemeral public key
    r.recvuntil(b'Server ephemeral random:\n')
    server_random = r.recvline().strip()
    r.recvuntil(b'Server ephemeral key:\n')

    server_cert = b""
    while True:
        data = r.recvline()
        if data == b'\n': break
        server_cert += data

    server_cert = serialization.load_pem_public_key(server_cert)
    # Load client epehmeral private key
    with open("client-ecdhkey.pem", "rb") as f:
        client_ephemeral_private_key = serialization.load_pem_private_key(
            f.read(),
            None,
            default_backend()
        )

    # Calculate shared key
    server_ephemeral_secret = client_ephemeral_private_key.exchange(ec.ECDH(), server_cert)

    # Exchange cert and key
    with open("server-ecdhcert.pem", "rb") as f:
        server_public_key = x509.load_pem_x509_certificate(f.read())
        server_public_key = server_public_key.public_key()

    with open("guest-ecdhkey.pem", "rb") as f:
        client_key = serialization.load_pem_private_key(f.read(), None)
        
    server_secret = client_key.exchange(ec.ECDH(), server_public_key)

    derived_key = HKDF(algorithm=hashes.SHA256(),
                    length=32,
                    salt=b'SaltyMcSaltFace',
                    info=b"mytls").derive(
                        server_ephemeral_secret +
                        server_secret +
                        bytes(16).hex().encode() +
                        server_random
                    )

    client_hmac = hmac.HMAC(derived_key, hashes.SHA256())
    client_hmac.update(b'client myTLS successful!')
    r.sendlineafter(b'Please provide the client HMAC:\n', client_hmac.finalize().hex().encode())

    server_hmac = hmac.HMAC(derived_key, hashes.SHA256())
    server_hmac.update(b'server myTLS successful!')
    r.recvuntil(b'Server HMAC:\n')
    assert server_hmac.finalize().hex() == r.recvline().strip().decode()

    ciphertext = r.recvline() # now ignore
    ctx = r.recvline().strip().decode()
    print_decrypted(ctx, server_random, derived_key)
    storage_slot = r.sendline(print_encrypted(key_path, server_random, derived_key).encode())
    ctx = r.recvline().strip().decode()
    print_decrypted(ctx, server_random, derived_key)

    overwrite_payload = "A"*(240 - len(known))
    secret = r.sendline(print_encrypted(overwrite_payload, server_random, derived_key).encode())
    prev_hash = print_decrypted(
        r.recvline().strip().decode(),
        server_random,
        derived_key)
    #print(prev_hash)
    prev_hash = prev_hash.split(b" ")[-1]
    print(prev_hash)

    # Phase 2
    ctx = r.recvline().strip().decode()
    print(print_decrypted(ctx, server_random, derived_key))
    storage_slot = r.sendline(print_encrypted(key_path, server_random, derived_key).encode())
    ctx = r.recvline().strip().decode()
    print(print_decrypted(ctx, server_random, derived_key))

    #overwrite_payload = "A"*240
    secret = r.sendline(print_encrypted("A", server_random, derived_key).encode())
    prev_hash = print_decrypted(
        r.recvline().strip().decode(),
        server_random,
        derived_key)
    #print(prev_hash)
    prev_hash = prev_hash.split(b" ")[-1]
    print(prev_hash)

    for i in range(256):
        h = hashlib.new("sha256")
        h.update((overwrite_payload + chr(i) + known).encode())
        if h.hexdigest() == prev_hash.decode():
            known = chr(i) + known
            print("Found", i)
            break
    print(known)
    if len(known) == 241:
        break

r.close()
```

Sau khi đã có `server-ecdhkey.pem`, mình quay lại bypass phần kiểm tra subject của certificate. Trong các file cert được cho thì có `admin-ecdhcert.pem` là có subject chúng ta cần (CN=admin.tls). Mình đã có `server-ecdhcert.pem` và `server-ecdhkey.pem` (vừa leak) để tiến hành trao đổi khóa. Tuy nhiên `server-ecdhcert.pem` thì lại không có CN=admin.tls.

Ở đây mình gửi lên `admin-ecdhcert.pem`, nhưng khi tính khóa trao đổi thì sử dụng `server-ecdhkey.pem` (không gửi `server-ecdhcert.pem`) và nó đã work!!! Đọc writeup của mọi người thì họ gọi là KCI attack do tính chất trao đổi khóa Diffie-Hellman.

Mình sửa đổi một tí file trên để lấy flag (gửi lên cert là `admin-ecdhcert.pem` và dùng `server-ecdhkey` để tính `share_key`).

```python
from pwn import remote, context
from cryptography.hazmat.primitives import serialization
from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.asymmetric import ec
from cryptography.hazmat.primitives.asymmetric import rsa
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.primitives.kdf.hkdf import HKDF
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives import hmac
from cryptography import x509
import binascii
import hashlib

context.log_level = 'Debug'

def print_encrypted(message, iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  encryptor = cipher.encryptor()
  message = message.encode('utf-8')
  payload = encryptor.update(
      message + b'\x00' * (16 - len(message) % 16)) + encryptor.finalize()
  #print(binascii.hexlify(payload).decode('utf-8'))
  return binascii.hexlify(payload).decode('utf-8')


def print_decrypted(message, iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  decryptor = cipher.decryptor()
  #message = message.encode('utf-8')
  message = bytes.fromhex(message)
  payload = decryptor.update(message)
  return payload.strip(b"\x00")


def input_encrypted(iv, key):
  cipher = Cipher(
      algorithms.AES(key),
      modes.CBC(binascii.unhexlify(iv)))
  decryptor = cipher.decryptor()
  payload = input()
  payload = binascii.unhexlify(payload)
  res = decryptor.update(payload)
  return res.strip(b'\x00')


r = remote("mytls.2023.ctfcompetition.com", 1337)
r.recvuntil(b'Please provide the client certificate in PEM format:')
with open("admin-ecdhcert.pem", "rb") as f:
    for line in f.readlines():
        r.send(line)
r.sendline()

# Exchange ECDH
r.sendlineafter(b'Please provide the ephemeral client random:', bytes(16).hex().encode())
r.recvuntil(b'Please provide the ephemeral client key:')
with open("client-ecdhcert.pem", "rb") as f:
    for line in f.readlines():
        r.send(line)
r.sendline()

# Get server ephemeral public key
r.recvuntil(b'Server ephemeral random:\n')
server_random = r.recvline().strip()
r.recvuntil(b'Server ephemeral key:\n')

server_cert = b""
while True:
    data = r.recvline()
    if data == b'\n': break
    server_cert += data

server_cert = serialization.load_pem_public_key(server_cert)
# Load client epehmeral private key
with open("client-ecdhkey.pem", "rb") as f:
    client_secret = serialization.load_pem_private_key(
        f.read(),
        None,
        default_backend()
    )

# Calculate shared key
server_ephemeral_secret = client_secret.exchange(ec.ECDH(), server_cert)

# Exchange cert and key
with open("admin-ecdhcert.pem", "rb") as f:
    server_public_key = x509.load_pem_x509_certificate(f.read())
    server_public_key = server_public_key.public_key()

with open("server-ecdhkey.pem", "rb") as f:
    client_key = serialization.load_pem_private_key(f.read(), None)
server_secret = client_key.exchange(ec.ECDH(), server_public_key)

derived_key = HKDF(algorithm=hashes.SHA256(),
                length=32,
                salt=b'SaltyMcSaltFace',
                info=b"mytls").derive(
                    server_ephemeral_secret +
                    server_secret +
                    bytes(16).hex().encode() +
                    server_random
                )

client_hmac = hmac.HMAC(derived_key, hashes.SHA256())
client_hmac.update(b'client myTLS successful!')
r.sendlineafter(b'Please provide the client HMAC:\n', client_hmac.finalize().hex().encode())

server_hmac = hmac.HMAC(derived_key, hashes.SHA256())
server_hmac.update(b'server myTLS successful!')
r.recvuntil(b'Server HMAC:\n')
assert server_hmac.finalize().hex() == r.recvline().strip().decode()

ciphertext = r.recvline().strip().decode() # now ignore
print(print_decrypted(ciphertext, server_random, derived_key))
r.close()

# b'Hello admin! CTF{KeyC0mpromiseAll0w51mpersonation}\n'
```

### PRIMES

```python
# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

def to_bits(m):
    _bin = lambda b : [1 if b & (1 << n) else 0 for n in range(7)]
    return sum([_bin(b) for b in m], [])

def gen_primes(r, n):
    primes = Primes()[:n]
    bound = prod(primes[n - r:])
    return primes, next_prime(bound)

def prod_exp(p, q, b):
    return prod([p[i]^b[i] for i in range(len(p))]) % q

def encode(r, n, m):
    p, q = gen_primes(r, n)
    return p, q, prod_exp(p, q, to_bits(m))

m = b"I have a sweet flag for you: CTF{YkDOLIStjpjP5Am1SXDt5d2r9es3b5KZP47v8rXF}"
p, q, x = encode(131, 7*len(m), m)
print(f'q = 0x{q:X}\nx = 0x{x:X}')

# q = 0xD2F8711CB5502C512ACEA59BE181A8FCF12F183B540D9A6998BF66370F9538F7E39FC507545DAD9AA2E71D3313F0B4408695A0A2C03A790662A9BD01650533C584C90779B73604FB8157F0AB7C9A82E724700E5937D9FF5FCF1EE3BE1EDD7E07B4C0F035A58CC2B9DB8B79F176F595C1B0E90B7957309B96106A50A01B78171599B41C8744BCB1C0E6A24F60AE8946D37F4D4BD8CF286A336E1022996B3BA3918E4D808627D0315BFE291AEB884CBE98BB620DAA735B0467F3287D158231D
# x = 0x947062E712C031ADD0B60416D3B87D54B50C1EFBC8DBB87346F960B242AF3DF6DD47406FEC98053A967D28FE91B130FF0FE93689122931F0BA6E73A3E9E6C873B8E2344A459244D1295E99A241E59E1EEA796E9738E6B1EDEED3D91AE6747E8ECA634C030B90B02BAF8AE0088058F6994C7CAC232835AC72D8B23A96F10EF03D74F82C49D4513423DAC298698094B5C631B9C7C62850C498330E9D112BB9CAA574AEE6B0E5E66D5B234B23C755AC1719B4B68133E680A7BCF48B4CFD0924D
```

Đề bài cho mình một dãy các số nguyên tố $p_i$ cố định và một số nguyên tố $q$.

Giả sử plaintext được biểu diễn ở dạng chuỗi bit $b = (b_1, b_2, \ldots, b_n)$ thì ciphertext sẽ là $x = \prod\limits_{i=1}^n p_i^{b_i} \bmod q$.

Tuy nhiên message $m$ mà đề cho không encrypt ra $x$ tương ứng, mình sẽ gọi là $y$. Nghĩa là nếu biểu diễn $m = (m_1, m_2, \ldots, m_n)$ thì mình có $y = \prod\limits_{i=1}^n p_i^{m_i} \bmod q$. Ở đây $m$ và flag có cùng độ dài và sự sai lệch bit không đáng kể.

Hmm, sai lệch bit không đáng kể? :v

Đặt

$$e = x y^{-1} = \prod_{i=1}^n p_i^{b_i - m_i} = \prod_{i=1}^n p_i^{e_i} \bmod q.$$

Khi đó $e_i \in \{-1, 0, 1\}$.

Suy ra $e = nd^{-1} \bmod q$ với $n$ và $d$ phân tích được thành lũy thừa dương của các $p_i$, từ đó tồn tại $s \in \mathbb{Z}$ để $ed = n + sq$.

Do $\lvert ed - sq \rvert = n$ nên tương đương với $\Bigg\lvert \dfrac{ed}{qd} - \dfrac{sq}{qd} \Bigg\rvert = \dfrac{n}{qd}$, hay $\Bigg\lvert \dfrac{e}{q} - \dfrac{s}{d} \Bigg\rvert = \dfrac{n}{qd}$.

Bài này dựa trên ý tưởng [xấp xỉ Diophantine](https://en.wikipedia.org/wiki/Diophantine\_approximation). Ở đây điều kiện để tồn tại chuỗi liên phân số hội tụ là $nd < \dfrac{q}{2}$. Khi đó $\dfrac{s}{d}$ là liên phân số hội tụ dần tới $\dfrac{1}{d^2}$ do $\dfrac{n}{qd} < \dfrac{1}{d^2}$.

Sử dụng SageMath mình có thể tìm được dãy các phân số $\dfrac{s_j}{d_j}$ hội tụ tới $\dfrac{1}{d^2}$. Do đó chiến thuật để giải bài này là tìm $d_j$ mà có thể phân tích thành lũy thừa không âm của các $p_i$ (tương ứng $y$). Sau đó với $d_j e$ mà cũng có thể phân tích thành lũy thừa không âm của các $p_i$ (tương ứng với $x$) thì ta sẽ tìm được phân tích tốt nhất để sửa các bit error $e_i$.

```python
def to_bits(m):
    _bin = lambda b : [1 if b & (1 << n) else 0 for n in range(7)]
    return sum([_bin(b) for b in m], [])

def from_bits(b):
    _byte = lambda c : bytes([sum([c[i] << i for i in range(7)])])
    return b''.join([_byte(b[i:i+7]) for i in range(0, len(b), 7)])

def gen_primes(r, n):
    primes = Primes()[:n]
    bound = prod(primes[n - r:])
    return primes, next_prime(bound)

def bitxor(a, b):
    return [a[i] ^^ b[i] for i in range(len(a))]

def prod_exp(p, q, b):
    return prod([p[i]^b[i] for i in range(len(p))]) % q

def encode(r, n, m):
    p, q = gen_primes(r, n)
    return p, q, prod_exp(p, q, to_bits(m))

def cfactor(primes, x):
    res = []
    if x == 1: return None
    for p in primes:
        if x % p == 0:
            res.append(p)
            x //= p
    return res if x == 1 else None

m = b"I have a sweet flag for you: CTF{YkDOLIStjpjP5Am1SXDt5d2r9es3b5KZP47v8rXF}"
#p, q, x = encode(131, 7*len(m), m)

q = 0xD2F8711CB5502C512ACEA59BE181A8FCF12F183B540D9A6998BF66370F9538F7E39FC507545DAD9AA2E71D3313F0B4408695A0A2C03A790662A9BD01650533C584C90779B73604FB8157F0AB7C9A82E724700E5937D9FF5FCF1EE3BE1EDD7E07B4C0F035A58CC2B9DB8B79F176F595C1B0E90B7957309B96106A50A01B78171599B41C8744BCB1C0E6A24F60AE8946D37F4D4BD8CF286A336E1022996B3BA3918E4D808627D0315BFE291AEB884CBE98BB620DAA735B0467F3287D158231D
X = 0x947062E712C031ADD0B60416D3B87D54B50C1EFBC8DBB87346F960B242AF3DF6DD47406FEC98053A967D28FE91B130FF0FE93689122931F0BA6E73A3E9E6C873B8E2344A459244D1295E99A241E59E1EEA796E9738E6B1EDEED3D91AE6747E8ECA634C030B90B02BAF8AE0088058F6994C7CAC232835AC72D8B23A96F10EF03D74F82C49D4513423DAC298698094B5C631B9C7C62850C498330E9D112BB9CAA574AEE6B0E5E66D5B234B23C755AC1719B4B68133E680A7BCF48B4CFD0924D
p = Primes()[:7*len(m)]
b = to_bits(m)
Y = prod_exp(p, q, b)
E = X * pow(Y, -1, q) % q
C = continued_fraction(E/q)
for c in C.convergents():
    k = c.denominator() # D
    l = k*E % q
    if k != 0 and l != 0:
        F = cfactor(p, k)
        Fp = cfactor(p, l)
        if F is not None and Fp is not None:
            mask = [0] * len(p)
            for i in range(len(p)):
                if p[i] in F+Fp:
                    mask[i] = 1
            x = bitxor(b, mask)
            print(from_bits(x))
```
