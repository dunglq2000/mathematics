## TJCTF 2024 phần 2

Phần này trình bày các bài mình làm sau khi giải kết thúc (có tham khảo writeup).

### 1. c-8

Đề bài cho mình các file `enc.py`, `dec.py`, `re_plaus`, `plausibly.deniable`. Với hint là affine cipher và modulo `n = 18446744073709551629` mình cần khôi phục lại bốn file trên.

Do $n$ có $65$ bit nên việc mã hóa theo mã affine sẽ mã hóa $8$ bytes một lần ra $9$ bytes của ciphertext. Các bạn cũng có thể thấy rằng byte đầu của mỗi đoạn $9$ bytes các file trên là `0x00` hoặc `0x01`.

Mã affine có dạng $y = ax + b \bmod n$ với $a$ và $b$ là hai số chưa biết cần đi tìm. Mình đã có $y$ và cần dự đoán $x$ nào sẽ mã hóa ra $y$ tương ứng. Đoạn đầu của các file mã hóa với Python thường sẽ dùng các thư viện như `pycryptodome`. Mình thử một loạt các kiểu import và tìm ra phần đầu sẽ là

```python
from Crypto.Cipher import AES
```

Mình chỉ cần $16$ bytes ở trên thôi là được. Dựa vào đó mình khôi phục lại $a$ và $b$ rồi decrypt bốn file ban đầu.

### 2. u-235

Lát viết

### 3. titanium-isopropoxide

Bài này mã hóa bằng file C++ với thuật toán khá phức tạp.

```cpp
#include <iostream>
#include <cinttypes>
#include <string>
#include <filesystem>
#include <fstream>
#include <sys/stat.h>
#include <vector>
#include <cstring>

void get_urandom(char* arr, int num) {
	std::ifstream urandom("/dev/urandom", std::ios::in | std::ios::binary);
	if (urandom)
	{
		urandom.read(arr, num); 
		if (urandom) 
		{
		}
		else 
		{
			std::cerr << "Failed to read from /dev/urandom" << std::endl;
		}
		urandom.close(); 
	}
	else 
	{
		std::cerr << "Failed to open /dev/urandom" << std::endl;
	}
}

using namespace std;
using namespace std::filesystem;

typedef uint8_t Byte;

void make_key(Byte *S)
{
	//SCREW YOU
	char rand_key[64];
	int key_size = 64;

	get_urandom(rand_key, key_size);

	for (int i = 0; i < 255; i++)
		S[i] = i;

	Byte j = 0;
	for (int i = 0; i < 255; i++)
	{
		j = (j ^ S[i] ^ rand_key[i % key_size]) % 256;
		std::swap(S[i], S[j]);
	}
}

Byte S_box[256] = {24, 250, 101, 19, 98, 246, 141, 58, 129, 74, 227, 160, 55, 167, 62, 57, 237, 156, 32, 46, 90, 67, 22, 3, 149, 212, 36, 210, 27, 99, 168, 109, 125, 52, 173, 184, 214, 86, 112, 70, 5, 252, 6, 170, 30, 251, 103, 43, 244, 213, 211, 198, 16, 242, 65, 118, 68, 233, 148, 18, 61, 17, 48, 80, 187, 206, 72, 171, 234, 140, 116, 35, 107, 130, 113, 199, 51, 114, 232, 134, 215, 197, 31, 150, 247, 79, 26, 110, 142, 29, 9, 117, 248, 186, 105, 120, 15, 179, 207, 128, 10, 254, 83, 222, 178, 123, 100, 39, 228, 84, 93, 97, 60, 94, 180, 146, 185, 38, 203, 235, 249, 89, 226, 1, 106, 12, 216, 221, 8, 45, 13, 2, 14, 75, 49, 33, 127, 163, 111, 85, 255, 253, 166, 151, 40, 23, 194, 34, 139, 95, 145, 193, 159, 133, 69, 245, 196, 102, 91, 11, 157, 96, 47, 152, 154, 59, 181, 28, 126, 200, 158, 88, 224, 231, 41, 190, 240, 191, 188, 143, 164, 189, 217, 54, 66, 241, 209, 104, 78, 87, 82, 230, 182, 220, 53, 147, 21, 136, 76, 0, 115, 169, 71, 44, 223, 175, 92, 25, 177, 64, 201, 77, 138, 144, 204, 229, 81, 20, 183, 205, 124, 243, 4, 172, 174, 108, 132, 176, 135, 161, 162, 7, 236, 195, 238, 56, 42, 131, 218, 155, 121, 153, 239, 50, 219, 225, 37, 202, 63, 137, 192, 208, 119, 122, 165, 73};

void enc(Byte *S, Byte *out, int amount)
{
	Byte i = 0;
	Byte j = 0;
	int ctr = 0;
	while (ctr < amount)
	{
		i = (i * j + i*j) % 256;
		j = (j | (i + S[j])) % 256;
		std::swap(S[(i*j) % 256],S[j]);
		Byte K = (S[i] & (~S[j]));
		out[ctr] ^= S_box[K];
		ctr++;
	}
}

float num[256];

Byte key[256];
int main()
{

	std::string path = current_path();

	std::vector<std::string> files;
	for (const auto &file : directory_iterator(path))
		files.push_back(std::string(file.path()));


	for (const auto &file : files)
	{
		std::cout << file << "\n";
		struct stat results;
		std::ifstream in(file);
		std::ofstream out(file + ".enc", std::ofstream::binary);
		if (stat(file.c_str(), &results) == 0)
		{
			uint8_t *buffer = new uint8_t[results.st_size];
			in.read((char *)buffer, results.st_size);

			make_key(key);
			enc(key, buffer, results.st_size);

			out.write((char *)buffer, results.st_size);
			delete[] buffer;
		}
		in.close();
		out.close();
	}

	return 0;
}
```

Bug ở bài này là key được tạo ra từ S-box không đủ mạnh. Sử dụng known-plaintext là flag format `tjctf{` và XOR với $6$ bytes đầu của ciphertext của hai file mình:

```python
flag2 = open("flag2.txt.enc", "rb").read()
flag3 = open("flag3.txt.enc", "rb").read()

def xor(a, b):
    return bytes(x^y for x, y in zip(a, b))

known_plaintext = b"tjctf{"

key = xor(flag2, known_plaintext)

f2 = []
f3 = []
for i in range(len(flag2)):
    f2.append(key[i % len(key)] ^ flag2[i])
    f3.append(key[i % len(key)] ^ flag3[i])

print(bytes(f2))
print(bytes(f3))
```

Kết quả mình thu được:

```
b'tjctf{\xa5%is_c\xbe)e_is\x8e;ery_\xb3,d_be\xb2,use_\xa8"u_ca\xbf\x12see_\xa1(ngui\xbf>_thr\xbe8gh_i\xa50\n'
b"\xc5'\x9dD\xa8k\xc4\xa0\x08\xf6>\xe6\xdf\xac\x04\xda\x08\xf6\xef\xbe\x04\xf7\x18\xda\xd2\xa9\x05\xda\x03\xe0\xd3\xa9\x14\xf6\x04\xda\xc9\xa7\x14\xda\x02\xe4\xde\x97\x12\xe0\x04\xda\xc0\xad\x0f\xe2\x14\xec\xde\xbb>\xf1\t\xf7\xdf\xbd\x06\xed>\xec\xc4\xb5k"
```

Mình thấy rằng `flag2` khá giống với đoạn văn có nghĩa. Sau dấu `{` là từ `this` (vì có sẵn chữ `is`), sau dấu `_` là `cube`. Như vậy, mình XOR đoạn `tjctf{this_cube` thì sẽ thấy được key:

```
b'<U\xed\x18\xed\x18\xed\x18\xed\x18\xed\x18\xf7\x1e\xed'
```

Mình thấy rằng key bắt đầu bởi `<U` và lặp lại cặp byte `\xed\x18`. Do đó mình có thể decrypt ra flag.

```python
flag2 = open("flag2.txt.enc", "rb").read()

def xor(a, b):
    return bytes(x^y for x, y in zip(a, b))

known_plaintext = b"tjctf{"

key = xor(flag2, known_plaintext)

while len(key) != 70:
    key += b"\xed\x18"

f2 = []
for i in range(len(flag2)):
    f2.append(key[i % len(key)] ^ flag2[i])

print(bytes(f2))
```

### 4. lithium-stearate

Sau khi giải kết thúc một pro đã hint cho mình: Slide attack

Tác giả bài này cho ba file: `common.hpp`, `main.cpp` và `output2.txt`. Mình sẽ không để file `common.hpp` ở đây vì cái hàm `ksch` dài quá mức :v.

```cpp
// main.cpp
#include "common.hpp"

int main()
{
	std::cout << "Hello world!\n";

	readflag();

	auto st = std::chrono::high_resolution_clock::now();

	std::vector<std::pair<Word, Word>> pairs;

	for (int i = 0; i < 18; i++)
	{
		Word p = getRand();
		Word c = oracle(p);
		pairs.push_back({ p, c });
	}

	// Redacted cheese pair generation because I want you to be happy

	for (int i = 0; i < 20; i++)
	{
		swap(pairs[getRand() % 20], pairs[getRand() % 20]);
	}

	std::cout << "OUTPUT.TXT STARTS HERE\n\n";

	for (auto& pair : pairs)
	{
		std::cout << "Plaintext, ciphertext: " << pair.first << " " << pair.second << "\n";
	}

	for (int i = 0; i < 20; i++)
	{
		std::cout << "Flag, ciphertext: " << flag[i] << "\n";
	}

	std::cout << "OUTPUT.TXT ENDS HERE\n\n";
	return 1;
}
```

Bài này mình được cho $20$ cặp plaintext-ciphertext cùng với ciphertext của flag. Thông tin về cipher:

- độ dài block là $16$ bits ($2$ bytes);
- độ dài khóa là $64$ bits ($8$ bytes);
- số vòng thực hiện là $100000$ vòng.

Hàm mã hóa:

```cpp
Word encrypt(Word in, Key k)
{
	Word out = in;
	for (int i = 0; i < rounds; i++)
	{
		out = r(out, ksch(k, i));
	}
	return out;
}
```

Trong đó `rounds = 100000` và `ksch` là key schedule sinh ra subkey cho mỗi vòng.

#### a. round function

Round function là hàm `r` với cấu trúc như sau:

```cpp
Word r(Word in, RKey kin)
{
	RKey k = kin;
	in ^= (k & 0xffff) ^ ((k >> 16) & 0xffff);
	return P_f(S_f(in));
}
```

Trong đó, `P_f` và `S_f` là hai hàm:

```cpp
Word S_f(Word in)
{
	return (Sbox[in >> 8] << 8) | Sbox[in & 0xff];
}

Word P_f(Word in)
{
	int r = 3;
	//std::cout << "in " << in << "\n";
	Word out = 0;
	out |= (in >> 8) & 0xff;
	out |= (in & 0xff) << 8;
	out ^= out >> 8;
	//std::cout << "out " << out << "\n";

	
	Word out2 = 0;
	out2 |= out >> r;
	out2 |= out << (16 - r);
	//std::cout << "out2 " << out2 << "\n";

	return out2;
}
```

Như vậy, `S_f` là hàm sử dụng S-box cho trước, và `P_f` là hàm hoán vị. Mình kí hiệu hai hàm này là $S_f$ và $P_f$.

Như vậy round function có dạng $out = P_f(S_f(out \oplus k))$, trong đó $r$ là số $16$ bits và $k$ cũng là số $16$ bits. Ở đây lưu ý rằng tham số thứ hai của `r` là số $32$ bits nhưng thực chất là lấy nửa đầu XOR nửa cuối, như vậy key được dùng có $16$ bits.

#### b. key schedule

Thuật toán sinh khóa `ksch` lấy đầu vào là khóa ban đầu $8$ bytes và vòng hiện tại $i$ để sinh ra khóa $k_i$. Khi thử in ra tất cả $1000000$ khóa khi mã hóa một plaintext bất kì thì chúng ta có thể thấy rằng **chỉ có đúng bốn subkey xoay vòng**.

Kết hợp với lúc nãy mình chỉ ra, mỗi round function lấy vào key $32$ bits nhưng thực chất chỉ là $16$ bits. Như vậy nếu bruteforce cả bốn vòng với bốn subkeys thì sẽ cần $16 \times 4 = 64$ bits. À thì nó cũng chả khác việc key ban đầu có $64$ bits :))) nên chúng ta sẽ không bruteforce kiểu này.

Chúng ta sẽ xem kỹ hơn hàm sinh khóa con `ksch`.

```cpp
RKey ksch(Key k, int i)
{
	// .............
	k |= 0xff << 24;
	k |= 0xffULL << (24 + 32);
	// .............
}
```

Đoạn trên cho thấy rằng, sau một hồi biến đổi, hàm `ksch` sẽ set bit thứ 3 và thứ 7 của biến `k` thành `0xff`, nghĩa là `k` lúc này có dạng `0xff------ff------` ($64$ bits).

```cpp
RKey ksch(Key k, int i)
{
	// .............
	if (i == 0)
	{
		r = k & 0xffffffff;
		r ^= 1162466901;
		r ^= r >> 16;
		r *= 3726821653;
	}
	if (i == 1)
	{
		r = ((k >> 32) & 0xffffffff) ^ (k & 0xffffffff);
		r ^= 3811777446;
		r = (r * 1240568533);
	}
	if (i == 2)
	{
		r = ((k >> 32) & 0xffffffff) ^ (k & 0xffffffff);
		r ^= 3915669785;
		r = (r * 1247778533);
	}
	if (i == 3)
	{
		r = ((k >> 32) & 0xffffffff) ^ (k & 0xffffffff);
		r ^= 3140176925;
		r = (r * 1934965865);
	}

	return r;
}
```

Ở phần kế của hàm `ksch` có $3/4$ trường hợp `r` là XOR của $32$ bits cao và $32$ bits thấp. Ở trên mình đã phân tích rằng bytes thứ 3 và thứ 7 của `k` sẽ là `0xff` nên khi XOR như vậy sẽ triệt tiêu byte đầu tiên của `r` nên `r` chỉ còn $24$ bits và chúng ta sẽ bruteforce ở đây.

Trong trường hợp `i = 0` thì chương trình cũng chỉ lấy $32$ bits thấp thôi nhưng chúng ta có thể bỏ qua. Lý do sẽ được trình bày ở phần sau.

#### c. slide attack

*Giới thiệu qua loa:* slide attack là phương pháp tấn công block cipher thông qua việc chọn các cặp plaintext-ciphertext $(P, C)$ và  $(P', C')$ mà $P' = F(P)$ và $C' = F(C)$ với $F(x)$ là hàm nào đó. Khi thỏa mãn các điều kiện trên thì ta có thể thực hiện slide attack.

Để tìm hàm $F(x)$ như vậy thì phụ thuộc vào cipher nào. Thông thường hàm $F(x)$ sẽ chứa một hoặc nhiều round, trong đó chứa tất cả khóa con của cipher.

**Ví dụ.** Xét mô hình cipher đơn giản sau:

$$P \xrightarrow{K_0} O_1 \xrightarrow{K_1} O_2 \xrightarrow{K_0} O_3 \xrightarrow{K_1} O_3 = C$$

Như vậy hàm $F(x)$ ở đây sẽ chứa hai subkey là $K_0$ và $K_1$. Do đó sơ đồ của $F$ sẽ là:

$$P \xrightarrow{F} O_2 \xrightarrow{F} C$$

Giả sử với một cặp plaintext-ciphertext khác là:

$$P' \xrightarrow{K_0} O_1 \xrightarrow{K_1} O_2 \xrightarrow{K_0} O_3 \xrightarrow{K_1} O_3 = C'$$

hay tương đương là

$$P' \xrightarrow{F} O'_2 \xrightarrow{F} C'$$

Slide attack lúc này sẽ hoạt động nếu $P' = O_2 = F(P)$ và $C' = F(C)$. Khi vẽ ra sẽ có dạng:

$$\begin{align*}
	P & \xrightarrow{F} & O_2 & \xrightarrow{F} & C & \\
	& & P' & \xrightarrow{F} & O_2' & \xrightarrow{F} & C'
\end{align*}$$

Quay lại bài lithium-stearate này, do chỉ có bốn subkeys nên có thể xem hàm $F$ ở trên có dạng:

$$F(P, K) = G(G(G(G(P, K_0), K_1), K_2), K_3) = P'$$

Trong đó $K$ là khóa ban đầu $64$ bits và mỗi $K_i$ là khóa con $32$ bits. Hàm $G(x, k) = P_f(S_f(x \oplus k))$ là round function.

Như vậy chiến thuật để giải bài này là:

- Tìm trong $20$ cặp plaintext-ciphertext đề cho các cặp $(P, C)$ và $(P', C')$ sao cho $F(P, K) = P'$ và $F(C, K) = C'$.
- Từ hai cặp plaintext-ciphertext trên khôi phục khóa $K$.

Tuy nhiên việc này khó khăn vì không có khóa $K$ thì không kiểm tra được điều kiện $F(P, K) = P'$. Do đó chúng ta sẽ làm ngược lại.

Như ở trên đã phân tích, $K_1$, $K_2$ và $K_3$ được sinh ra từ một `k` có $24$ bits, do đó chúng ta bruteforce các `k` như vậy và tính ra $K_1$, $K_2$ và $K_3$ tương ứng.

Với mỗi hai plaintext $P_i$ và $P_j$ ta tính $K_0$ theo $K_0 = S_f^{-1}(P^{-1}(T)) \oplus P$, với 

$$T = G^{-1}(G^{-1}(G^{-1}(P', K_3), K_2), K_1).$$

Khi đã có đủ $K_0$, $K_1$, $K_2$ và $K_3$, mình sẽ kiểm tra điều kiện $C' = F(C, K)$. Nếu thỏa mãn thì mình có được một cặp **slid pair** và sẽ thử mã hóa hai cặp plaintext-ciphertext bất kì để xem việc mã hóa với khóa có đúng không.

Khi tìm được khóa rồi thì mình giải mã lại flag.

```cpp
// findkey.cpp
#include <iostream>
#include <fstream>
#include <map>
#include <omp.h>
#include <inttypes.h>
#include <vector>
#include <utility>

using namespace std;

constexpr int rounds = 100000;

typedef uint8_t Byte;

typedef uint16_t Word;

typedef uint32_t RKey;

typedef uint64_t Key;

Byte Sbox[256] = { 58, 66, 209, 131, 35, 82, 37, 249, 78, 74, 129, 168, 244, 207, 155, 102, 175, 22, 248, 63, 24, 172, 114, 4, 216, 105, 116, 44, 196, 137, 42, 45, 118, 110, 124, 90, 139, 119, 56, 238, 3, 121, 65, 112, 30, 146, 36, 202, 94, 19, 163, 188, 68, 104, 170, 10, 227, 16, 69, 165, 210, 41, 52, 8, 115, 240, 49, 197, 174, 195, 89, 134, 246, 43, 62, 91, 199, 83, 96, 101, 223, 92, 11, 128, 7, 99, 160, 225, 109, 28, 47, 204, 190, 14, 192, 86, 226, 181, 140, 54, 2, 239, 200, 171, 71, 184, 254, 29, 23, 85, 141, 176, 222, 189, 205, 122, 72, 87, 81, 211, 133, 117, 6, 169, 130, 212, 247, 25, 156, 127, 31, 93, 67, 142, 206, 107, 158, 95, 60, 12, 193, 27, 79, 232, 229, 177, 149, 100, 167, 243, 235, 20, 26, 32, 46, 231, 40, 157, 34, 230, 253, 18, 153, 80, 213, 39, 159, 125, 64, 203, 241, 138, 220, 132, 53, 147, 98, 97, 0, 185, 123, 77, 150, 218, 161, 136, 13, 61, 173, 21, 111, 251, 50, 221, 208, 250, 15, 178, 182, 59, 70, 194, 214, 236, 33, 75, 108, 9, 255, 38, 113, 5, 217, 237, 224, 152, 215, 201, 242, 164, 198, 145, 144, 57, 186, 106, 245, 233, 162, 126, 103, 143, 135, 120, 84, 180, 228, 154, 76, 219, 234, 183, 88, 1, 252, 51, 166, 48, 191, 148, 151, 55, 73, 17, 179, 187 };

Byte invSbox[256] = { 178, 243, 100, 40, 23, 211, 122, 84, 63, 207, 55, 82, 139, 186, 93, 196, 57, 253, 161, 49, 151, 189, 17, 108, 20, 127, 152, 141, 89, 107, 44, 130, 153, 204, 158, 4, 46, 6, 209, 165, 156, 61, 30, 73, 27, 31, 154, 90, 247, 66, 192, 245, 62, 174, 99, 251, 38, 223, 0, 199, 138, 187, 74, 19, 168, 42, 1, 132, 52, 58, 200, 104, 116, 252, 9, 205, 238, 181, 8, 142, 163, 118, 5, 77, 234, 109, 95, 117, 242, 70, 35, 75, 81, 131, 48, 137, 78, 177, 176, 85, 147, 79, 15, 230, 53, 25, 225, 135, 206, 88, 33, 190, 43, 210, 22, 64, 26, 121, 32, 37, 233, 41, 115, 180, 34, 167, 229, 129, 83, 10, 124, 3, 173, 120, 71, 232, 185, 29, 171, 36, 98, 110, 133, 231, 222, 221, 45, 175, 249, 146, 182, 250, 215, 162, 237, 14, 128, 157, 136, 166, 86, 184, 228, 50, 219, 59, 246, 148, 11, 123, 54, 103, 21, 188, 68, 16, 111, 145, 197, 254, 235, 97, 198, 241, 105, 179, 224, 255, 51, 113, 92, 248, 94, 140, 201, 69, 28, 67, 220, 76, 102, 217, 47, 169, 91, 114, 134, 13, 194, 2, 60, 119, 125, 164, 202, 216, 24, 212, 183, 239, 172, 193, 112, 80, 214, 87, 96, 56, 236, 144, 159, 155, 143, 227, 240, 150, 203, 213, 39, 101, 65, 170, 218, 149, 12, 226, 72, 126, 18, 7, 195, 191, 244, 160, 106, 208 };

Word S_f(Word in)
{
	return (Sbox[in >> 8] << 8) | Sbox[in & 0xff];
}

Word P_f(Word in)
{
	int r = 3;

	Word out = 0;
	out |= (in >> 8) & 0xff;
	out |= (in & 0xff) << 8;
	out ^= out >> 8;
	
	Word out2 = 0;
	out2 |= out >> r;
	out2 |= out << (16 - r);

	return out2;
}

Word S_f_inv(Word in)
{
    return (invSbox[in >> 8] << 8) | invSbox[in & 0xff];
}

Word P_f_inv(Word in)
{
    int r = 3;
    Word out2 = 0;
    out2 |= in >> (16 - r);
    out2 |= in << r;

    Word out = out2;
    out ^= out >> 8;
    out = (out << 8) | (out >> 8);
    return out;
}

uint16_t G(uint16_t in, uint16_t kin)
{
    return P_f(S_f(in ^ kin));
}

uint16_t round(uint16_t in, uint32_t kin)
{
	uint32_t k = kin;
	in ^= (k & 0xffff) ^ ((k >> 16) & 0xffff);
	return P_f(S_f(in));
}

uint16_t round_inv(uint16_t in, uint32_t kin)
{
    uint32_t k = (kin & 0xffff) ^ ((kin >> 16) & 0xffff);
    return S_f_inv(P_f_inv(in)) ^ (k & 0xffff);
}

uint16_t G_inv(uint16_t ct, uint32_t key)
{
    uint32_t key1 = key ^ 3811777446;
    key1 = (key1 * 1240568533);

    uint32_t key2 = key ^ 3915669785;
    key2 = (key2 * 1247778533);

    uint32_t key3 = key ^ 3140176925;
    key3 = (key3 * 1934965865);

    return round_inv(round_inv(round_inv(ct, key3), key2), key1);
}

int main()
{
    std::vector<std::pair<uint16_t, uint16_t>> pairs;
    pairs.push_back({ 46797, 26174});
    pairs.push_back({ 33355, 8806 });
    pairs.push_back({ 12127, 30892});
    pairs.push_back({ 36367, 9717});
    pairs.push_back({ 44727, 24673});
    pairs.push_back({ 3529, 47408});
    pairs.push_back({ 31925, 20694});
    pairs.push_back({ 28137, 56468});
    pairs.push_back({ 52803, 52774});
    pairs.push_back({ 44410, 46131});
    pairs.push_back({ 45425, 12595});
    pairs.push_back({ 54554, 26552});
    pairs.push_back({ 12635, 58598});
    pairs.push_back({ 12932, 46831});
    pairs.push_back({ 8597, 32794});
    pairs.push_back({ 62968, 279});
    pairs.push_back({ 26520, 54428});
    pairs.push_back({ 13693, 32325});
    pairs.push_back({ 49153, 21047});
    pairs.push_back({ 11475, 62360});

    int T = pairs.size();

    std::vector<uint16_t> pts = {};
    std::vector<uint16_t> cts = {};
    uint16_t O[65536] = { 0 };
    for (uint16_t i = 0; i < T; i++) 
    {
        pts.push_back(pairs[i].first);
        cts.push_back(pairs[i].second);
    }

    for (uint16_t i = 0; i < T; i++)
    {
        if(S_f_inv(S_f(pts[i])) != pts[i])
        {
            cout << "S_f_inv wrong!" << endl;
            return 1;
        }
        if (P_f_inv(P_f(pts[i])) != pts[i])
        {   
            cout << "P_f_inv wrong!" << endl; 
            return 1;
        }
        if (round_inv(round(pts[i], 0xdeadbeaf), 0xdeadbeaf) != pts[i])
        {   
            cout << "round_inv wrong!" << endl; 
            return 1;
        }
    }

    for (uint16_t i = 0; i < T; i++)
    {
        for (uint32_t key0 = 0; key0 < 0x10000; key0++)
            O[P_f(S_f(pts[i] ^ key0))] = key0;

        for (uint16_t j = 0; j < T; j++)
        {
            if (i == j) continue;

            #pragma omp parallel for
            for (uint32_t key = 0; key < 0x1000000; key++)
            {
                uint32_t key0 = S_f_inv(P_f_inv(G_inv(pts[j], key))) ^ pts[i];

                uint32_t key1 = key ^ 3811777446;
                key1 = (key1 * 1240568533);

                uint32_t key2 = key ^ 3915669785;
		        key2 = (key2 * 1247778533);

                uint32_t key3 = key ^ 3140176925;
		        key3 = (key3 * 1934965865);

                uint16_t rk0 = (key0 & 0xffff);
                uint16_t rk1 = ((key1 >> 16) & 0xffff) ^ (key1 & 0xffff);
                uint16_t rk2 = ((key2 >> 16) & 0xffff) ^ (key2 & 0xffff);
                uint16_t rk3 = ((key3 >> 16) & 0xffff) ^ (key3 & 0xffff);

                uint16_t c = cts[i];
                c = P_f(S_f(c ^ rk0));
                c = P_f(S_f(c ^ rk1));
                c = P_f(S_f(c ^ rk2));
                c = P_f(S_f(c ^ rk3));
                if (c == cts[j])
                {
                    uint16_t pt = pts[0];
                    for (uint16_t r = 0; r < (100000 / 4); r++)
                    {
                        pt = G(G(G(G(pt, rk0), rk1), rk2), rk3);
                    }
                    if (pt == cts[0])
                    {
                        uint16_t pt2 = pts[15];
                        for (uint16_t r = 0; r < (100000 / 4); r++)
                        {
                            pt2 = G(G(G(G(pt2, rk0), rk1), rk2), rk3);
                        }
                        if (pt2 == cts[15])
                        {
                            cout << "Found key!" << endl;
                            cout << rk0 << ", " << rk1 << ", " << rk2 << ", " << rk3 << endl;
                            exit(0);
                        }
                    }
                    
                }
            }
        }
    }
    return 0;
}
```

Sau khi chạy `findkey.cpp` thì mình tìm được key là $11892, 8704, 3384, 38922$. Sau đó mình decrypt ra flag. Ở đây mình compile với flag `-O3` và `openmp` vì mình không có nhiều kinh nghiệm dùng GCC lắm :))) Code cũng sẽ chạy nhanh hơn nếu sử dụng các flag khác, cũng như C++ khác như 11, ...

Lệnh compile: `g++ -O3 findkey.cpp -o findkey -fopenmp`.

```cpp
// decrypt.cpp
#include <iostream>
#include <fstream>
#include <map>
#include <omp.h>
#include "common.hpp"

Word S_f_inv(Word in)
{
    return (invSbox[in >> 8] << 8) | invSbox[in & 0xff];
}

Word P_f_inv(Word in)
{
    int r = 3;
    Word out2 = 0;
    out2 |= in >> (16 - r);
    out2 |= in << r;

    Word out = out2;
    out ^= out >> 8;
    out = (out << 8) | (out >> 8);
    return out;
}

int main()
{
    std::vector<uint16_t> cts = {
        12210, 15594, 18592, 47466, 23526, 48987, 44863,
        19536, 52633, 21435, 34703, 5383, 16355, 46571, 
        59850, 35352, 16108, 38178, 50671, 64648
    };

    uint16_t rk0 = 11892, rk1 = 8704, rk2 = 3384, rk3 = 38922;
    std::vector<uint16_t> pts = {};
    for (uint16_t i = 0; i < cts.size(); i++)
    {
        uint16_t pt = cts[i];
        for (uint16_t r = 0; r < (100000 / 4); r++)
        {
            pt = S_f_inv(P_f_inv(pt)) ^ rk3;
            pt = S_f_inv(P_f_inv(pt)) ^ rk2;
            pt = S_f_inv(P_f_inv(pt)) ^ rk1;
            pt = S_f_inv(P_f_inv(pt)) ^ rk0;
        }
        char x = pt & 0xff;
        char y = pt >> 8;
        std::cout << x << y;
    }
    std::cout << std::endl;

    return 0;
}
```