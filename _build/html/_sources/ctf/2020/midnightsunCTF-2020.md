## Midnight Sun CTF 2020

### rsa_yay

```python
while True:
    p = random_prime(2**512)
    q = ZZ(int(hex(p)[::-1], 16))
    if q.is_prime():
        break

# hex(p*q)
# '7ef80c5df74e6fecf7031e1f00fbbb74c16dfebe9f6ecd29091d51cac41e30465777f5e3f1f291ea82256a72276db682b539e463a6d9111cf6e2f61e50a9280ca506a0803d2a911914a385ac6079b7c6ec58d6c19248c894e67faddf96a8b88b365f16e7cc4bc6e2b4389fa7555706ab4119199ec20e9928f75393c5dc386c65'
# hex(ciphertext)
# '3ea5b2827eaabaec8e6e1d62c6bb3338f537e36d5fd94e5258577e3a729e071aa745195c9c3e88cb8b46d29614cb83414ac7bf59574e55c280276ba1645fdcabb7839cdac4d352c5d2637d3a46b5ee3c0dec7d0402404aa13525719292f65a451452328ccbd8a0b3412ab738191c1f3118206b36692b980abe092486edc38488'
```

Nếu biết $k$ bit cao nhất của $p$ và $q$, gọi là $ph$ và $qh$ thì ta có chặn

$$ph \cdot qh \cdot 2^{1024-2k} \leqslant n < (ph+1) \cdot (qh + 1) \cdot 2^{1024-2k}$$

Khi đó, ta brute $12$ bit thấp nhất của $p$ và tính nghịch đảo của từng trường hợp trong modulo $2^{12}$. Nghịch đảo này chính là $12$ bit thấp nhất của $q$ và suy ra được $12$ bit cao nhất của $p$ và $q$.


```python
from gmpy2 import *
import binascii

n = 0x7ef80c5df74e6fecf7031e1f00fbbb74c16dfebe9f6ecd29091d51cac41e30465777f5e3f1f291ea82256a72276db682b539e463a6d9111cf6e2f61e50a9280ca506a0803d2a911914a385ac6079b7c6ec58d6c19248c894e67faddf96a8b88b365f16e7cc4bc6e2b4389fa7555706ab4119199ec20e9928f75393c5dc386c65
cipher = 0x3ea5b2827eaabaec8e6e1d62c6bb3338f537e36d5fd94e5258577e3a729e071aa745195c9c3e88cb8b46d29614cb83414ac7bf59574e55c280276ba1645fdcabb7839cdac4d352c5d2637d3a46b5ee3c0dec7d0402404aa13525719292f65a451452328ccbd8a0b3412ab738191c1f3118206b36692b980abe092486edc38488

def reverse_hex(x,n):
    y = 0
    for i in range(n):
        y = y*16 + x % 16
        x //= 16
    return y

cur = []

# Find all cases for lowest 12 bits
for i in range(1, 4096, 2): # i is lowest 12 bits of p
    t = pow(i, -1, 4096) * (n % 4096) % 4096 # t is lowest 12 bits of q
    assert t * i % 4096 == n % 4096
    t2 = reverse_hex(t,3) # t2 is highest 12 bits of q
    i2 = reverse_hex(i,3) # i2 is highest 12 bits of p
    l = i2 * t2 << (4 * 125 * 2)
    r = (i2 + 1) * (t2 + 1) << (4 * 125 * 2)
    if l <= n <= r: # check where n is in the range
        cur.append(i)

# Current digit (in hex)
for c in range(4, 65):
    nc = []
    mod = 16**c
    for x in cur:
        for y in range(16):
            i = x + y * 16**(c-1) # i is lowest 4c bits of p
            t = pow(i, -1, mod) * (n % mod) % mod # t is lowest 4c bits of q
            assert t*i%mod==n%mod
            t2 = reverse_hex(t, c) # t2 is highest 4c bits of q
            i2 = reverse_hex(i, c) # i2 is highest 4c bits of p
            l = i2 * t2 << (4 * (128 - c) * 2)
            r = (i2 + 1) * (t2 + 1) << (4 * (128 - c) * 2)
            if l <= n <= r: # check where n is in the range
                nc.append(i)
    cur=nc

# Find real solution
c = 64
mod = 16**c
for i in cur:
    t = pow(i, -1, mod) * (n % mod) % mod
    assert t * i % mod == n % mod
    t2 = reverse_hex(t, c)
    i2 = reverse_hex(i, c)
    p = t2 << 256 | i
    q = i2 << 256 | t
    if p * q == n:
        break

e = 65537
d = pow(e, -1, (p - 1) * (q - 1))
o = pow(cipher, d, p*q)
print(binascii.unhexlify(hex(o)[2:]))
```

    b'midnight{d1vid3_and_c0nqu3r}x/\xda\xc9\xc4y\xb4\xc5!\x14\xc4p\xfal<a\x00\xd9m\xae\xb0k\xf8\xe0\xb31\xd9\xe6J\xcd\xaf|\x0b\xde6\xe2\xe8|>\xb8\xa2\x03\xa6\x92\xf6\xf3i\x10\xbb\x04\xc4Ha\x83d\x9d}6S\x88K\xba\tp\xed\xa3\xe2\xaf3\xc9\xae\xa9\xafF\xe5\x0c?\xae\x99\xae\x12\xb1\x9fO\xd2\xbc\x86\xedi\xab\xfc\xe7I\x82\xba\xfee\xba\xf0\xed'
    
