## NSUCRYPTO 2020

### Problem 1 (R1). 2020

#### Đề bài

Cho dãy $S$, cipher machine có thể thêm vào $S$ hoặc xóa khỏi $S$ dãy con với dạng 11, 101, 1001, 10...01. Machine cũng có thể xóa khỏi $S$ hoặc thêm vào $S$ một dãy liên tục các số 0.

Smith biểu diễn số 2020 dưới dạng nhị phân và sử dụng hai cipher machine để biến đổi. Máy đầu tiên trả về dạng nhị phân của số 1984, máy thứ hai trả về dạng nhị phân của số 2021.

Smith chắc chắn rằng một trong hai máy đã bị lỗi. Làm sao anh ấy biết được?

#### Giải

Ta viết các số 2020, 1984 và 2021 dưới dạng nhị phân.

Như vậy $2020 = 11111100100$, $1984 = 11111000000$ và $2021 = 11111100101$.

Đặt $2020 = 11111 \underbrace{1001}_A 00$ thì nếu ta xóa dãy $A$ khỏi 2020 và thêm vào vị trí đó bốn chữ số 0 thì ta có 1984. Như vậy máy đầu tiên hoạt động bình thường.

Việc thêm vào hoặc xóa đi 11, 101, 1001, ... thì số lượng bit 1 tăng giảm đi một lượng chẵn còn thêm bớt 0 không ảnh hưởng. Do 2020 và 2021 có số lượng bit 1 khác tính chẵn lẻ nên không thể biến đổi từ 2020 thành 2021.

Như vậy máy thứ hai bị hỏng.

### Problem 4 (R1). RGB

#### Đề bài

Trong một server có hai biến $a$ và $b$. Khi server nhận query dạng "RED", "GREEN" hoặc "BLUE" thì giá trị của chúng sẽ thay đổi theo query nhận được.

Cụ thể hơn, cặp $(a, b)$ biến thành $(a + 18b, 18a - b)$ nếu query là "RED", biến thành $(17a + 6b, -6a + 17b)$ nếu query là "GREEN" và biến thành $(-10a-15b, 15a-10b)$ nếu là "BLUE".

Khi $a$ hoặc $b$ trở thành bội của 324 thì nó được reset thành 0. Khi $(a, b) = (0, 0)$ thì server crash.

Ban đầu, $(a, b)$ được khai báo là $(20, 20)$. Chứng minh rằng server sẽ không bao giờ crash dù có bao nhiêu query được gửi tới.

#### Giải

Phép biến đổi tương đương với phép nhân ma trận $(a, b) \to (a, b) \bm{A}$ với $\bm{A}$ là ma trận xác định bởi

1. $\bm{A} = \begin{pmatrix} 1 & 18 \\ 18 & -1 \end{pmatrix}$ khi query là "RED".
2. $\bm{A} = \begin{pmatrix} 17 & -6 \\ 6 & 17 \end{pmatrix}$ khi query là "GREEN".
3. $\bm{A} = \begin{pmatrix} -10 & 15 \\ -15 & -10 \end{pmatrix}$ khi query là "BLUE".

Kết quả cuối là việc thực hiện liên tiếp các phép nhân có dạng

$$(a, b) \cdot \bm{A}_1 \bm{A}_2 \cdots \bm{A}_r$$

với $\bm{A}_i$ là một trong ba ma trận trên.

Đặt $\bm{A}_1 \cdots \bm{A}_r = B$ thì phép nhân tương đương với $(a, b) \cdot \begin{pmatrix} X & Y \\ Z & T \end{pmatrix} = (324, 324)$. Trong đó $X, Y, Z, T \in \mathbb{Z}$.

Điều này tương đương với $a \cdot X + b \cdot Z = 324$ và $a \cdot Y + b \cdot T = 324$. Suy ra $20 (X + Z) = 324$ và $20 (Y + T) = 324$. Nhưng điều này không thể xảy ra vì 324 không chia hết 20.

Như vậy server không bao giờ crash dù có thực hiện bao nhiêu query đi nữa.

### Problem 1. Poly

#### Đề bài

Bob phát minh một thuật toán tên là *POLY*. Với $x$ là plaintext thì ciphertext là $y = p(x)$, với $p(x)$ là đa thức với hệ số nguyên.

Đồng nghiệp của Bob muốn kiểm tra thuật toán. Khi encrypt 20 thì Bob nhận được 7. Sau đó anh đồng nghiệp encrypt 15 thì nhận được 5. Anh ta kết luận rằng thuật toán đã bị cài đặt sai. Chuyện gì đã xảy ra?

#### Giải

Giả sử đa thức là

$$p(x) = a_n x^n + a_{n-1} x^{n-1} + \cdots + a_1 x + a_0.$$

Khi đó $p(20) = a_n 20^n + a_{n-1} 20^{n-1} + \cdots + a_1 \cdot 20 + a_0 = 7$.

Tương tự $p(15) = a_n 15^n + a_{n-1} 15^{n-1} + \cdots + a_1 \cdot 15 + a_0 = 5$.

Suy ra $p(20) - p(15) = 2$ mà $p(20) - p(15)$ chia hết cho $20 - 15 = 5$ nên vô lý vì 2 không chia hết cho 5. Như vậy thuật toán đã bị cài đặt sai.