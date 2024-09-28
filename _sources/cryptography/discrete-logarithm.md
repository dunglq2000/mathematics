# Discrete logarithm

## Các thuật toán tính discrete logarithm

Thuật toán Baby-Step-Giant-Step (BSGS) giúp tính discrete logarithm trên nhóm cyclic với order là số nguyên tố.

````{prf:algorithm} Thuật toán Baby-Step-Giant-Step
**Input:** Nhóm cyclic $G$ có order $n$, generator $g$ và phần tử $h \in G$.

**Output:** Số $x$ duy nhất thuộc $\{ 0, 1, \ldots, n-1 \}$ thỏa $g^x = h$.

1. $m \gets \lfloor \sqrt{n} \rfloor$
2. for $j = 0$ to $m-1$
    1. Tính $g^j$. Lưu $(j, g^j)$ vào bảng.
3. Tính $g^{-m}$.
4. $\gamma \gets h$.
5. for $i = 0$ to $m-1$
    1. Kiểm tra điều kiện $\gamma = g^j$ với $j = 0, 1, \ldots, m-1$.
    2. Nếu điều kiện thỏa, trả về $im + j$.
    3. Nếu không, đặt $\gamma \gets \gamma \cdot g^{-m}$.
````

Khi order của cyclic group là lũy thừa một số nguyên tố thì ta dùng thuật toán Pohlig-Hellman.

````{prf:algorithm} Thuật toán Pohlig-Hellman
**Input:** Nhóm cyclic $G$ có order $n=p^e$, generator $g$ và phần tử $h \in G$.

**Output:** Số $x$ duy nhất thuộc $\{ 0, 1, \ldots, n-1 \}$ thỏa $g^x = h$.

1. Khởi tạo $x_0 = 0$.
2. Tính $\gamma = g^{p^{e-1}}$. Theo định lý Lagrange, $\gamma$ có order là $p$.
3. for $k = 0$ to $e-1$
    1. Tính $h_k = (g^{-x_k} \cdot h)^{e-1-k}$.
    2. Sử dụng thuật toán baby-step-giant-step, tìm $d_k \in \{ 0, 1, \ldots, p-1 \}$ sao cho $\gamma^{d_k} = h_k$. Bước này có độ phức tạp $O(\sqrt{p})$.
    3. Tính $x_{k+1} = x_k + p^k d_k$.
4. Trả về $x_e$ là kết quả cần tìm.
````
