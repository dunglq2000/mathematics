# Phép biến hình

```{contents}
:depth: 2
```

Trong thực tế chúng ta hay gặp các vấn đề về việc di dời một hình
nào đó sang một vị trí khác trong mặt phẳng, không gian và phải đảm bảo 
giữ nguyên một số quan hệ nhất định. Trong đó cơ bản nhất và được ứng dụng 
rộng rãi là phép dời hình và phép đồng dạng.

## Phép dời hình

````{prf:definition} Phép dời hình
Phép dời hình từ hình $\mathcal{H}$ thành hình $\mathcal{H}'$ là một ánh xạ $f$ biến mỗi điểm thuộc hình $\mathcal{H}$ thành điểm thuộc hình $\mathcal{H}'$ sao cho khoảng cách giữa 2 điểm bất kì trong $\mathcal{H}$ bảo toàn khi qua $\mathcal{H}'$.
````

Nói cách khác, với mọi điểm $A, B \in \mathcal{H}$, ánh xạ $f$ biến $A$ thành $A'$ và $B$ thành $B'$ ($A', B' \in \mathcal{H}'$) thì $A'B' = AB$.

Chúng ta thường thấy việc dời hình theo vector (dời theo 1 hướng nhất định), đối xứng qua trục, đối xứng qua tâm, quay quanh tâm hoặc trục nào đó.

## Phép dời hình theo vector

Phép dời hình theo vector $\vec{v} \neq \vec{0}$ (phép tịnh tiến) biến
điểm $A$ thành điểm $A'$ sao cho $\overrightarrow{AA'} = \vec{v}$.

Dễ thấy đây là phép dời hình vì với mọi $A, B$ biến thành $A', B'$ ta có $\overrightarrow{A'B'} = \overrightarrow{A'A} + \overrightarrow{AB} + \overrightarrow{BB'}$ mà ta có $\overrightarrow{A'A} = -\vec{v} = -\overrightarrow{BB'}$ nên $\overrightarrow{A'B'} = \overrightarrow{AB}$. Vector bằng nhau thì độ dài cũng bằng nhau. Ta có điều phải chứng minh.

```{figure} ../figures/geometric_transform/by_vector.jpg

Tịnh tiến theo vector $\vec{a}$
```

## Phép đối xứng qua đường thẳng cố định

Cho đường thẳng cố đinh $(d)$. Phép đối xứng qua đường thẳng $(d)$ biến điểm $A$ thành điểm $A'$ sao cho $AA'$ cắt $(d)$ tại trung điểm $AA'$ và đường thẳng đi qua $AA'$ vuông góc với $(d)$.

```{figure} ../figures/geometric_transform/by_line.jpg

Đối xứng qua đường thẳng $(d)$
```

## Phép đối xứng qua tâm cố định

Cho điểm cố định $O$. Phép đối xứng tâm $O$ biến điểm $A$ thành điểm $A'$ sao cho $\overrightarrow{OA} = -\overrightarrow{OA'}$. Nói cách khác $O$ là trung điểm
đoạn thẳng $AA'$.

## Phép quay quanh tâm cố định

Cho điểm cố định $O$. Phép quay (mặc định là ngược chiều đồng hồ) quanh tâm $O$ theo một góc cố định $\varphi$ biến điểm $A$ thành điểm $A'$ sao cho $\widehat{(\overrightarrow{OA}, \overrightarrow{OA'})} = \varphi$.

Trên mặt phẳng chúng ta có thể biểu diễn phép quay dưới hệ tọa độ như sau.

Giả sử vector $\overrightarrow{OA}$ có độ dài là $r$ và hợp với trục $Ox$ một góc $\alpha$.

Khi đó, giả sử tọa độ của $\overrightarrow{OA} = (x, y)$ thì ta có 

$$\begin{align*}
    x & = r \cos \alpha \\
    y & = r \sin \alpha
\end{align*}$$

Nếu ta quay vector này quanh gốc tọa độ, ngược chiều kim đồng hồ một góc $\varphi$ thì 
thực ra góc (mới) hợp bởi vector $\overrightarrow{OA'}$ và trục $Ox$ là $\alpha + \varphi$.
Do đó

$$\begin{align*}
    x' & = r \cos (\alpha + \varphi) \\
    y' & = r \sin (\alpha + \varphi)
\end{align*}$$

Khi khai triển ra

$$\begin{align*}
    x' & = r \cos \alpha \cos \varphi - r \sin \alpha \sin \varphi
= x \cos \varphi - y \sin \varphi \\
    y' & = r \sin \alpha \cos \varphi + r \cos \alpha \sin \varphi 
= y \cos \varphi + x \sin \varphi
\end{align*}$$

Dễ thấy, phép quay bảo toàn khoảng cách từ tâm $O$ tới điểm đó. Nghĩa là $OA = OA'$.

```{figure} ../figures/geometric_transform/rotation.jpg
```

## Phép biến hình trên mặt phẳng tọa độ

Gọi $A = (x, y)$ là tọa độ ban đầu của điểm và $A' = f(A) = (x', y')$ là tọa độ điểm $A'$, là kết quả của phép biến hình $f$ lên điểm $A$.

Chúng ta lần lượt xét các phép biến hình đã liệt kê ở trên và chuyển về phép nhân ma trận.

Các phép nhân ma trận cho phép chúng ta hợp các phép biến đổi liên tiếp thành một biến đổi lớn.

Giả sử $A_T$ là ma trận ứng với phép tịnh tiến, $A_R$ là ma trận ứng với phép quay.

Khi đó với phép nhân ma trận, nếu ta muốn thực hiện liên tiếp phép tịnh tiến và phép quay thì ta có $A_T \cdot A_R$.

Hợp các phép dời hình không có tính giao hoán, cũng như phép nhân ma trận. Do đó thứ tự thực hiện phép dời hình khác nhau thì thứ tự nhân ma trận cũng khác nhau.

Một yêu cầu về phép biến đổi tuyến tính là không có vector tự do, nghĩa là biến đổi có dạng

$$\begin{pmatrix}
x' \\ y'
\end{pmatrix} = A \cdot \begin{pmatrix}
x \\ y
\end{pmatrix},$$

với $A$ là ma trận $n \times n$.

### Phép dời hình theo vector

Đặt $\vec{v} = (a, b)$ là vector tịnh tiến. Khi đó $\overrightarrow{AA'} = \vec{v}$ sẽ tương đương với

$$x' - x = a, \quad y' - y = b,$$

hay tương đương với $x' = x + a$ và $y' = y + b$.

Dễ thấy rằng kết quả có thể viết ở dạng:

$$\begin{pmatrix}
    x' \\ y'
\end{pmatrix} = \begin{pmatrix}
    1 & 0 \\ 0 & 1
\end{pmatrix} \cdot \begin{pmatrix}
    x \\ y
\end{pmatrix} + \begin{pmatrix}
    a \\ b
\end{pmatrix}$$

Tuy nhiên chúng ta cần một biến đổi tuyến tính (không có vector $\begin{pmatrix} a \\ b \end{pmatrix}$).

Lúc này, thay vì sử dụng ma trận $2 \times 2$ thì ta chuyển thành $3 \times 3$ và công thức trở thành:

$$\begin{equation*}
    \begin{pmatrix}
        x' \\ y' \\ 1
    \end{pmatrix} = \begin{pmatrix}
        1 & 0 & a \\
        0 & 1 & b \\
        0 & 0 & 1
    \end{pmatrix} \cdot \begin{pmatrix}
        x \\ y \\ 1
    \end{pmatrix}
\end{equation*}$$

Ma trận $\begin{pmatrix}
    1 & 0 & a \\ 0 & 1 & b \\ 0 & 0 & 1
\end{pmatrix}$ là ma trận tịnh tiến (translation vector) tương ứng với phép tịnh tiến điểm $A = (x, y)$ theo vector $\vec{v} = (a, b)$.

### Phép đối xứng qua đường thẳng cố định

(Chưa viết)

### Phép đối xứng qua tâm cố định

Theo định nghĩa ở trên, giả sử tâm $O$ có tọa độ $(a, b)$. Điều kiện $\overrightarrow{OA} = \overrightarrow{OA'}$ tương đương với:

$$\begin{equation*}
    x - a = -(x' - a), \quad y - a = -(y' - b),
\end{equation*}$$

hay tương đương với

$$\begin{equation*}
    x' = -x + 2a, \quad y' = -y + 2b.
\end{equation*}$$

Tương tự bên trên, ta muốn một phép nhân ma trận mà không cộng thêm vector ngoài.

$$\begin{equation*}
    \begin{pmatrix}
        x' \\ y' \\ 1
    \end{pmatrix} = \begin{pmatrix}
        -1 & 0 & 2a \\
        0 & -1 & 2b \\
        0 & 0 & 1
    \end{pmatrix} \cdot \begin{pmatrix}
        x \\ y \\ 1
    \end{pmatrix}
\end{equation*}$$

Như vậy, ma trận $\begin{pmatrix}
    -1 & 0 & 2a \\
    0 & -1 & 2b \\
    0 & 0 & 1
\end{pmatrix}$ là ma trận đối xứng qua tâm $O = (a, b)$.

### Phép quay quanh tâm cố định

Từ công thức của phép quay quanh tâm là gốc tọa độ:

$$\begin{pmatrix}
    x' \\ y'
\end{pmatrix} = \begin{pmatrix}
    \cos \varphi & -\sin \varphi \\
    \sin \varphi & \cos \varphi
\end{pmatrix} \begin{pmatrix}
    x \\ y
\end{pmatrix}$$

Tuy nhiên trong các phép biến đổi trên ta cần ma trận $3 \times 3$ thay vì $2 \times 2$ nên phép quay cũng cần ma trận $3 \times 3$ để có thể hợp với các phép biến hình khác.

$$\begin{equation*}
    \begin{pmatrix}
        x' \\ y' \\ 1
    \end{pmatrix} = \begin{pmatrix}
        \cos\phi & -\sin\phi & 0 \\
        \sin\phi & \cos\phi & 0 \\
        0 & 0 & 1
    \end{pmatrix} \cdot \begin{pmatrix}
        x \\ y \\ 1
    \end{pmatrix}
\end{equation*}$$

Như vậy ma trận $\begin{pmatrix}
    \cos\phi & -\sin\phi & 0 \\
    \sin\phi & \cos\phi & 0 \\
    0 & 0 & 1
\end{pmatrix}$ thể hiện phép quay quanh tâm $O$ tại gốc tọa độ.