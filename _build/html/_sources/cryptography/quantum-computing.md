# Quantum computing

## Qubit và toán tử quantum

Trên máy tính hiện nay, đơn vị xử lý cơ bản là bit (0 hoặc 1). Trong máy tính lượng tử, đơn vị tính toán là qubit (quantum bit).

## Qubit

Mỗi qubit $\lvert \psi \rangle$ được biểu diễn dưới dạng tổ hợp tuyến tính của cơ sở gồm $\lvert 0 \rangle = (1, 0)$ và $\lvert 1 \rangle = (0, 1)$. Khi đó qubit $\lvert \psi \rangle = \alpha \lvert 0 \rangle + \beta \lvert 1 \rangle$. Ở đây $\alpha, \beta \in \mathbb{C}$ (tập số phức).

Tích của $n$ qubit là các tổ hợp $\lvert 0, 0, \ldots, 0 \rangle$, $\lvert 0, 0, \ldots, 1 \rangle$, ..., $\lvert 1, 1, \ldots, 1 \rangle$. Ta cũng ký hiệu $\lvert 0 \rangle \otimes \lvert 1 \rangle = \lvert 01 \rangle$. 

````{prf:example}
Nếu $\lvert \psi \rangle = \alpha \lvert 0 \rangle + \beta \lvert 1 \rangle$ và $\lvert \Psi \rangle = \gamma \lvert 0 \rangle + \delta \lvert 1 \rangle$ thì

$$\begin{equation*}
    \lvert \psi \rangle \otimes \lvert \Psi \rangle = (\alpha \lvert 0 \rangle + \beta \lvert 1 \rangle) \otimes (\gamma \lvert 0 \rangle + \delta \lvert 1 \rangle) = \alpha \gamma \lvert 00 \rangle + \alpha \delta \lvert 0 1 \rangle + \beta \gamma \lvert 10 \rangle + \beta \delta \lvert 11 \rangle
\end{equation*}$$
````

Tiếp theo là **toán tử quantum** và tương ứng với nó là các cổng (gate) trên mạch.

Toán tử quantum tác động lên một qubit hoặc tích của nhiều qubit.

Qubit có dạng $\lvert \psi \rangle = a \lvert 0 \rangle + b \lvert 1 \rangle$. Ta có thể viết hệ số dưới dạng vector cột $\begin{pmatrix} a \\ b \end{pmatrix}$. Khi đó, toán tử quantum sẽ là một ma trận $2 \times 2$ biến đổi vector trên thành vector mới $\begin{pmatrix} c \\ d \end{pmatrix}$ tương ứng với qubit $\lvert \Psi \rangle = c \lvert 0 \rangle + d \lvert 1 \rangle$.

Nói cách khác, đặt toán tử quantum là ma trận $\mathcal{U} = \begin{pmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{pmatrix}$ thì ta có

$$\begin{equation*}
    \lvert \psi \rangle \to \lvert \Psi \rangle = \mathcal{U} \lvert \psi \rangle, \quad \begin{pmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{pmatrix} \cdot \begin{pmatrix} a \\ b \end{pmatrix} = \begin{pmatrix} c \\ d \end{pmatrix}
\end{equation*}$$

## Các toán tử quantum thường gặp

````{prf:definition} Toán tử đồng nhất
Toán tử đồng nhất identity giữ nguyên qubit đầu vào. Ma trận tương ứng là ma trận đơn vị $I = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$.
````

````{prf:definition} Toán tử NOT
Toán tử NOT có ma trận tương ứng là $\text{NOT} = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$. Khi đó $\text{NOT} \lvert \psi \rangle = b \lvert 0 \rangle + a \lvert 1 \rangle$ với $x \in \{ 0, 1 \}$.
````

Khi qubit là $\lvert 0 \rangle$ hoặc $\lvert 1 \rangle$, tác dụng của toán tử NOT là phép XOR nên ta có $\text{NOT} \lvert x \rangle = \lvert x \oplus 1 \rangle$.

````{prf:definition} Toán tử Hadamard
Ma trận của toán tử Hadamard là $H = \dfrac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & - 1 \end{pmatrix}$. 
````

````{prf:example}
Xét qubit $\lvert \psi \rangle = a \lvert 0 \rangle + b \lvert 1 \rangle$, toán tử Hadamard tương ứng với phép nhân ma trận

$$\begin{equation*}
    \dfrac{1}{\sqrt{2}} \begin{pmatrix} 1 & 1 \\ 1 & - 1 \end{pmatrix} \cdot \begin{pmatrix} a \\ b \end{pmatrix} = \begin{pmatrix} \dfrac{1}{\sqrt{2}} (a + b) \\ \dfrac{1}{\sqrt{2}} (a - b) \end{pmatrix}
\end{equation*}$$

Ta chuyển cột kết quả về lại dạng tổ hợp tuyến tính thì cổng Hadamard hoạt động trên qubit $\lvert \psi \rangle = a \lvert 0 \rangle + b \lvert 1 \rangle$ cho kết quả là

$$\begin{equation*}
    H \lvert \psi \rangle = H(a \lvert 0 \rangle + b \lvert 1 \rangle) = \dfrac{1}{\sqrt{2}} (a + b) \lvert 0 \rangle + \dfrac{1}{\sqrt{2}} (a - b) \lvert 1 \rangle
\end{equation*}$$
````

Nếu $\lvert \psi \rangle \equiv \lvert 0 \rangle$ thì tương đương với $a = 1, b = 0$. Ta có $H \lvert 0 \rangle = \dfrac{\lvert 0 \rangle + \lvert 1 \rangle}{\sqrt{2}}$.

Nếu $\lvert \psi \rangle \equiv \lvert 1 \rangle$ thì tương đương với $a = 0, b = 1$. Ta có $H \lvert 1 \rangle = \dfrac{\lvert 0 \rangle - \lvert 1 \rangle}{\sqrt{2}}$.

Tổng quát ta nhận thấy, với $x \in \{ 0, 1 \}$ thì $H \lvert x \rangle = \dfrac{\lvert 0 \rangle + (-1)^x \lvert 1 \rangle}{\sqrt{2}}$.

Ta thấy rằng toán tử ngược của toán tử Hadamard là chính nó.

Tiếp theo là toán tử thường được dùng nhất khi tính toán trên tích của nhiều qubit: toán tử control.

Như đã xem xét ở trên, tích của $n$ qubit sẽ có $2^n$ phần tử tương ứng các bộ $\lvert 0, 0, \ldots, 0, 0 \rangle$, $\lvert 0, 0, \ldots, 0, 1 \rangle$, ... Do đó toán tử control sẽ là ma trận kích thước $2^n \times 2^n$.


````{prf:definition} Toán tử control 
Gọi $\mathcal{U} = \begin{pmatrix} c_{11} & c_{12} \\ c_{21} & c_{22} \end{pmatrix}$ là toán tử tác động lên một qubit. Xét hai qubit là $\lvert x \rangle = a \lvert 0 \rangle + b \lvert 1 \rangle$ và $\lvert y \rangle = c \lvert 0 \rangle + d \lvert 1 \rangle$. Ta có tích

$$\begin{equation*}
    \lvert x \rangle \otimes \lvert y \rangle = ac \lvert 00 \rangle + ad \lvert 01 \rangle + bc \lvert 10 \rangle + bd \lvert 11 \rangle
\end{equation*}$$

Khi đó toán tử control có dạng ma trận là

$$\begin{equation*}
    c \mathcal{U} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & c_{11} & c_{12} \\ 0 & 0 & c_{21} & c_{22} \end{pmatrix}
\end{equation*}$$

Hay viết dưới dạng ma trận khối là $c \mathcal{U} = \begin{pmatrix} I & \mathcal{O} \\ \mathcal{O} & \mathcal{U} \end{pmatrix}$.
````

Ta cũng viết tích $\lvert x \rangle \otimes \lvert y \rangle$ dưới dạng vector cột (4 phần tử). Khi đó

$$\begin{equation*}
    \mathcal{U} (\lvert x \rangle \otimes \lvert y \rangle) = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & c_{11} & c_{12} \\ 0 & 0 & c_{21} & c_{22} \end{pmatrix} \cdot \begin{pmatrix} ac \\ ad \\ bc \\ bd \end{pmatrix} = \begin{pmatrix} ac \\ ad \\ c_{11} \cdot bc + c_{12} \cdot bd \\ c_{21} \cdot bc + c_{22} \cdot bd \end{pmatrix}
\end{equation*}$$

Hai phần tử đầu của vector kết quả không thay đổi, còn phần sau có "một phần" là $\mathcal{U} \lvert y \rangle$. Khi viết lại kết quả dưới dạng qubit thì

$$\begin{equation*}
    ac \lvert 00 \rangle + ad \lvert 01 \rangle + (c_{11} \cdot bc + c_{12} \cdot bd) \lvert 10 \rangle + (c_{21} \cdot bc + c_{22} \cdot bd) \lvert 11 \rangle
\end{equation*}$$

Ta có một số nhận xét sau đây.

Nếu $\lvert x \rangle \equiv \lvert 0 \rangle$, tức là $a = 1, b = 0$ thì tích trên tương ứng với $c \lvert 00 \rangle + d \lvert 01 \rangle + 0 \lvert 10 \rangle + 0 \lvert 11 \rangle = \lvert 0 \rangle \otimes (c \lvert 0 \rangle + d \lvert 1 \rangle) = \lvert x \rangle \otimes \lvert y \rangle$.

Nếu $\lvert x \rangle \equiv \lvert 1 \rangle$, tức là $a = 0, b = 1$ thì tích trên tương ứng với $0 \lvert 00 \rangle + 0 \lvert 01 \rangle + (c_{11} c + c_{12} d) \lvert 10 \rangle + (c_{21} c + c_{22} d) \lvert 11 \rangle = \lvert 1 \rangle \otimes ((c_{11} c + c_{12} d) \lvert 0 \rangle + (c_{21} c + c_{22} d) \lvert 1 \rangle) = \lvert 1 \rangle \otimes \mathcal{U} \lvert y \rangle = \lvert x \rangle \otimes \mathcal{U} \lvert y \rangle$.

Tổng kết lại, với $x \in \{ 0, 1\}$ thì

- nếu $x = 0$ thì $\lvert x \rangle \otimes \lvert y \rangle \to \lvert x \rangle \otimes \lvert y \rangle$.
- nếu $x = 1$ thì $\lvert x \rangle \otimes \lvert y \rangle \to \lvert x \rangle \otimes \mathcal{U} \lvert y \rangle$.

Tùy vào $x$ là 0 hay 1 mà toán tử quantum $\mathcal{U}$ sẽ bị bỏ qua hoặc xem xét. Ở đây qubit $\lvert x \rangle$ đóng vai trò điều khiển nên đây được gọi là toán tử control.

````{prf:definition} Toán tử control CNOT, Control NOT
Toán tử quantum CNOT có ma trận là

$$\begin{equation*}
    \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \end{pmatrix} = \begin{pmatrix} I & \mathcal{O} \\ \mathcal{O} & \text{NOT} \end{pmatrix}
\end{equation*}$$
````

Qubit $\lvert x \rangle$ với $x \in \{ 0, 1 \}$ đóng vai trò control cho qubit $\lvert y \rangle$. Khi $x \equiv 0$ thì $y$ giữ nguyên, hay $\lvert y \oplus 0 \rangle = \lvert y \oplus x \rangle$. Khi $x \equiv 1$ thì áp dụng cổng NOT bên trên, khi đó $y$ biến đổi thành $y \oplus 1 = y \oplus x$.