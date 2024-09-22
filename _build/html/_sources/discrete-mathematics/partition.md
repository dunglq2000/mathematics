# Phân hoạch

```{contents}
:depth: 2
```

## Số Stirling

### Số Stirling loại 1

Xét tập các hoán vị trên tập hữu hạn $n$ phần tử. Số hoán vị chứa $k$ chu trình độc lập là số Stirling loại 1, ký hiệu là $\mathcal{S}_n^{(k)}$.

Các bước khởi đầu là $\mathcal{S}_0^{(0)} = 1$ (có đúng một cách chia tập 0 phần tử vào 0 chu trình), $\mathcal{S}_n^{(0)} = \mathcal{S}_0^{(n)} = 0$ (không có cách nào chia tập $n$ phần tử vào 0 chu trình và chia tập 0 phần tử vào $n$ chu trình).

Công thức đệ quy của số Stirling là:

$$\begin{equation}
    \mathcal{S}_{n+1}^{(k)} = n \cdot \mathcal{S}_n^{(k)} + \mathcal{S}_{n}^{(k-1)}
\end{equation}$$

```{admonition} **Chứng minh.**
:class: danger, dropdown
Giả sử tập có $n+1$ phần tử là $A = \{ 1, 2, \ldots, n, n+1\}$. Khi đó để phân hoạch $n+1$ phần tử này vào $k$ chu trình độc lập thì có hai trường hợp:

1. Đầu tiên xếp các phần tử $1, 2, \ldots, n$ vào $k$ chu trình độc lập thì có $\mathcal{S}_n^{(k)}$ cách chọn. Tiếp theo ta cho phần tử $n+1$ vào một vị trí bất kì trong $k$ chu trình trên thì có $n$ cách chọn. Vậy trường hợp này là $n \cdot \mathcal{S}_n^{(k)}$.
2. Ta phân $n$ phần tử $1, 2, \ldots, n$ vào $k-1$ chu trình độc lập và phần tử $n+1$ sẽ vào chu trình thứ $k$. Trường hợp này có $\mathcal{S}_n^{(k-1)} \cdot 1$ cách chọn.

Như vậy tổng số cách phân $n+1$ phần tử vào $k$ chu trình độc lập là hợp của hai trường hợp trên. Ta có điều phải chứng minh.
```

````{prf:example}
Có bao nhiêu hoán vị của $\mathcal{S}_5$ chứa đúng ba chu trình độc lập?

Ta có các trường hợp sau:

1. Hoán vị có dạng $(1)(2)(3, 4, 5)$. Ta chọn hai phần tử làm hai chu trình độc lập, có $C^2_5 = 10$ cách chọn. Tiếp theo chọn ba phần tử cho chu trình cuối, có $2!$ cách chọn. Vậy trường hợp này có $10 \cdot 2 = 20$ cách chọn.
2. Hoán vị có dạng $(1)(2, 3)(4, 5)$. Ta chọn một phần tử làm chu trình độc lập có $C^1_5 = 5$ cách chọn. Tiếp theo chọn hai phần tử cho chu trình tiếp theo trong 4 phần tử còn lại, có $C^2_4 = 6$ cách chọn. Hai phần tử còn lại là $C^2_2 = 1$ cách chọn. Lưu ý là hai chu trình độc lập có thể đổi chỗ cho nhau nên cần chia thêm $2!$ nữa, ví dụ $(1, 2)(3, 4)$ hoàn toàn giống với $(3, 4)(1, 2)$. Số cách chọn cho trường hợp này là $5 \cdot 6 / 2 = 15$ cách chọn.

Như vậy số hoán vị của $\mathcal{S}_5$ chứa đúng ba chu trình độc lập là $20 + 15 = 35$.

Ta so sánh kết quả với số Stirling. Ta cần tìm $\mathcal{S}_5^{(3)}$.

Ta có:

$$\begin{align*}
    \mathcal{S}_5^{(3)} = & 4 \cdot \mathcal{S}_4^{(3)} + \mathcal{S}_4^{(2)} \\
        = & 4 \cdot \left(3 \cdot \mathcal{S}_3^{(3)} + \mathcal{S}_3^{(2)}\right) + 3 \cdot \mathcal{S}_3^{(2)} + \mathcal{S}_3^{(1)} \\
        = & 4 \cdot \left(3 \cdot 1  + 2 \cdot \mathcal{S}_2^{(2)} + \mathcal{S}_2^{(1)}\right) + 3 \cdot \left(2 \cdot \mathcal{S}_2^{(2)} + \mathcal{S}_2^{(1)}\right) + 2 \cdot \mathcal{S}_2^{(1)} + \mathcal{S}_2^{(0)} \\
        = & 4 \cdot \left(3 + 2 \cdot 1 + 1 \cdot \mathcal{S}_1^{(1)} + \mathcal{S}_1^{(0)}\right) + 3 \cdot \left(2 \cdot 1 + \mathcal{S}_1^{(1)} + \mathcal{S}_1^{(0)}\right) + \mathcal{S}_1^{(1)} + \mathcal{S}_1^{(0)} + 0 \\
        = & 4 \cdot (3 + 2 + 1) + 3 \cdot (2 + 1 + 0) + 2 \cdot 1 + 0 + 0 = 35
\end{align*}$$

Kết quả số Stirling khớp với việc giải bằng tổ hợp và không đòi hỏi các suy luận phức tạp.
````

````{prf:remark}
Số Stirling loại 1 cho phép tính số lượng phân hoạch theo đệ quy thay vì giải các bài toán tổ hợp phức tạp. Điều này hiệu quả khi các số $n$ và $k$ trở nên lớn.
````

Tính chất của số Stirling loại 1:

1. $\displaystyle{\sum_{k=1}^{n}\mathcal{S}_n^{(k)} = n!}$. Công thức này chỉ số hoán vị có thể có của một tập $n$ phần tử.

### Số Stirling loại 2

Số Stirling loại 2 thể hiện số cách phân bổ $n$ phần tử vào $k$ tập hợp rời nhau, ký hiệu là $s(n, k)$.

Công thức đệ quy của số Stirling loại 2 là:

$$\begin{equation}
    s(n+1, k) = k \cdot s(n, k) + s(n, k-1)
\end{equation}$$

```{admonition} **Chứng minh.**
:class: danger, dropdown
Cách chứng minh khá tương tự số Stirling loại 1. Tuy nhiên ở đây việc phân một phần tử vào một tập hợp không xét tới thứ tự, điều này khác với chu trình cần xem xét thứ tự. Như vậy ta vẫn có hai trường hợp

1. Phân các phần tử $1, 2, \ldots, n$ vào $k$ tập hợp. Sau đó phần tử $n+1$ sẽ được phân vào một trong $k$ tập đó nên có $k$ cách chọn.
2. Phân các phần tử $1, 2, \ldots, n$ vào $k-1$ tập hợp và phần tử $n+1$ vào tập hợp thứ $k+1$.

Từ đây ta có công thức số Stirling loại 2.
```

Các bước cơ sở cho số Stirling loại 2 cũng tương tự loại 1: $s(n, n) = 1$, $s(n, 0) = s(0, n) = 0$.
