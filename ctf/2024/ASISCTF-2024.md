## ASIS CTF 2024

Bài này mình làm sau khi giải kết thúc.

### Clement

```python
#!/usr/bin/env python3

import time
from functools import wraps
from Crypto.Util.number import *
from signal import *
from secret import rapid_factoreal_check, flag

def die(*args):
	pr(*args)
	quit()
	
def pr(*args):
	s = " ".join(map(str, args))
	sys.stdout.write(s + "\n")
	sys.stdout.flush()
	
def sc():
	return sys.stdin.buffer.readline()

class TimeoutError(Exception):
	pass

def exec_limit(mt):
	def decorator(func):
		@wraps(func)
		def wrapper(*args, **kwargs):
			def _handle_timeout(signum, frame):
				raise TimeoutError(f"Function execution time exceeded {mt} seconds.")
			old_handler = signal(SIGALRM, _handle_timeout)
			alarm(int(mt))
			try:
				result = func(*args, **kwargs)
			except TimeoutError:
				return False
			finally:
				signal(SIGALRM, old_handler)
			return result
		return wrapper
	return decorator

TIMEOUT = 3
@exec_limit(TIMEOUT)
def factoreal(n, k, b):
	if b: # When YOU have access to supercomputer!
		i, s = 1, 1
		while i < n + 1:
			s = (s * i) % k
			i += 1
		if (4 * s + n + 5) % k == 0:
			return True
		return False
	else: # Otherwise
		return rapid_factoreal_check(n)

def main():
	global secret, border
	border = "┃"
	pr(        "┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓")
	pr(border, "Welcome to Clement Crypto Challenge, we have gained access to a   ", border)
	pr(border, "very powerful supercomputer with high processing capabilities. Try", border)
	pr(border, "to connect to the app running on this computer and find the flag. ", border)
	pr(        "┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛")
	b, c, nbit, STEP = False, 0, 64, 19
	for level in range(STEP):
		pr(border, f"Your are at level {level + 1} of {STEP}")
		pr(border, f"Please submit an {nbit}-integer:")
		_n = sc().decode()
		try:
			_n = int(_n)
			_k = _n**2 + 4*_n + 3
		except:
			die(border, 'Your input is not integer! Bye!!')
		if _n.bit_length() == nbit:
			try:
				_b = factoreal(_n, _k, b)
			except TimeoutError:
				pass
		else:
			die(border, f"Your input integer is NOT {nbit}-bit! Bye!!") 
		if _b:
			c += 1
			nbit = int(1.1 * nbit) + getRandomRange(1, 12)
			if c >= STEP:
				die(border, f'Congratulation! You got the flag: {flag}')
		else:
			die(border, "Wrong response! Start again. Bye!!") 

if __name__ == '__main__':
	main()
```

Ở bài này chúng ta cần nhập vào số $n$. Chương trình sẽ tính $k = n^2 + 4 n + 3$.

Hàm `factoreal` sẽ kiểm tra $4 \cdot n! + n + 5 \equiv 0 \pmod k$ hay không.

Để giải bài này mình cần định lý Wilson:

```{admonition} Định lý Wilson
Nếu $p$ là số nguyên tố thì

$$(p-1)! \equiv -1 \pmod p$$
```

Do $k = n^2 + 4n + 3 = (n + 1) \cdot (n + 3)$, mình mong muốn tìm số $n$ thỏa mãn hai phương trình

$$\begin{align*}
    4 \cdot n! + n + 5 \equiv 0 \pmod{n+1} \\ 
    4 \cdot n! + n + 5 \equiv 0 \pmod{n+3}
\end{align*},$$

trong đó $n+1$ và $n+3$ là các số nguyên tố. Khi đó nghiệm trong modulo $k$ theo CRT sẽ là $0$.

Nếu $n + 1$ là số nguyên tố, theo định lý Wilson thì $n! \equiv -1 \pmod{n+1}$. Như vậy

$$4 \cdot n! + n + 5 \equiv 4 \cdot (-1) + (n + 1) + 4 \equiv -4 + 4 \equiv 0 \pmod{n+1}$$

Nếu $n + 3$ là số nguyên tố thì $(n+2)! \equiv -1 \pmod{n+3}$. Khi đó

$$\begin{align*}
    4 \cdot n! + n + 5 & \equiv 4 \cdot \dfrac{(n+3)!}{(n+2) \cdot (n+1)} + (n + 3) + 2 \pmod{n+3} \\
    & \equiv 4 \cdot \dfrac{(-1)}{(n + 2) \cdot (n + 1)} + 2 \equiv 0 \pmod{n+3}
\end{align*}$$

Như vậy nếu điều kiện cuối là $4 \cdot \dfrac{-1}{(n+2) \cdot (n+1)} + 2 \equiv 0 \pmod{n+3}$ thỏa mãn thì mình đã tìm được số $n$ cần thiết.

Đây là bài toán về coding với timeout nên chúng ta có thể lưu các số nguyên tố $t$ bit vào file trước khi remote tới server (precompute).