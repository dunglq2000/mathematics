# Xác suất thống kê

```{contents}
```

## Xác suất là gì?

````{prf:definition} Định nghĩa cổ điển của xác suất
Định nghĩa thống kê của xác suất nói rằng, giả sử trong một phép thử có $n$ khả năng có thể xảy ra. Xét một biến cố $A$ xảy ra khi thực hiện phép thử có $k$ khả năng xảy ra. Khi đó xác suất của biến cố $A$ ký hiệu là $P(A)$ và được tính:

$$P(A) = \frac{k}{n}$$
````

Dễ thấy, do biến cố $A$ là một trường hợp nhỏ trong tổng thể tất cả trường hợp khi thực hiện phép thử, nên $0 \leqslant k \leqslant n$. Nghĩa là:

$$0 \leqslant P(A) \leqslant 1$$

với mọi biến cố $A$ bất kì.

````{prf:example}
Xét phép thử tung hai đồng xu. Gọi $A$ là biến cố hai đồng xu cùng mặt.

Ta ký hiệu $S$ là đồng xu sấp, $N$ là đồng xu ngửa. Khi đó các trường hợp có thể xảy ra của phép thử là $S-S$, $S-N$, $N-S$, $N-N$ (4 trường hợp). 

Trong khi đó, các trường hợp có thể xảy ra của biến cố $A$ là $S-S$, $N-N$ (2 trường hợp).

Kết luận: $P(A) = \dfrac{2}{4} = \dfrac{1}{2}$.
````

Chúng ta gọi tập hợp tất cả các trường hợp khi thực hiện phép thử là **không gian mẫu** và ký hiệu là $\Omega$. Mỗi phần tử trong không gian mẫu được gọi là **biến cố sơ cấp**. Trong ví dụ trên:

$$\Omega = \{ S-S, S-N, N-S, N-N \}$$
    
Tập hợp các trường hợp có thể xảy ra của biến cố gọi là **không gian biến cố** và ký hiệu là $\Omega_A$. Trong ví dụ trên, $\Omega_A = \{S-S, N-N\}$.
    
Như vậy, $P(A) = \dfrac{|\Omega_A|}{|\Omega|}$.

````{prf:example}
Tung hai con súc sắc cân đối và đồng chất. Tính xác suất tổng số nút của hai con súc sắc bằng 4.

Việc tung mỗi con súc sắc có 6 trường hợp. Do đó $|\Omega| = 6^2 = 36$.

Gọi $A$ là biến cố tổng số nút của hai con súc sắc bằng 4. Ta có các trường hợp là $4=1+3=3+1=2+2$ (3 trường hợp).

Như vậy $|\Omega_A| = 3$ và $P(A) = \dfrac{3}{36} = \dfrac{1}{12}$
````

### Ba tiên đề về sự nhất quán của xác suất

**Tiên đề 1.** Nếu $A$ là một sự kiện và kí hiệu $P(A)$ là **xác suất của** $A$ thì:

$$\begin{equation}
0 \leqslant P(A) \leqslant 1
\end{equation}$$

**Tiên đề 2.** Nếu $A$ là một sự kiện và kí hiệu $\bar{A}$ là sự kiện phủ định của $A$ thì:

$$\begin{equation}
P(A) + P(\bar{A}) = 1
\end{equation}$$

**Tiên đề 3.** Với hai sự kiện $A$ và $B$, nếu hai sự kiện $A$ và $B$ không thể cùng xảy ra thì xác suất của sự kiện "xảy ra $A$ hoặc $B$" bằng tổng các xác suất của $A$ và $B$:

$$\begin{equation}
P(A \cap B) = 0 \Rightarrow P(A \cup B) = P(A) + P(B)
\end{equation}$$

### Không gian xác suất

````{prf:definition} Không gian xác suất
Một **không gian xác suất** là một tập hợp $\Omega$ cùng với:

1) Một họ $\mathcal{S}$ các tập con của $\Omega$, thỏa mãn các tính chất sau:
    - $\Omega \in \mathcal{S}$;
    - nếu $A, B \in \mathcal{S}$ thì $A \cup B \in \mathcal{S}$, $A \cap B \in \mathcal{S}$ và $\bar{A} = \Omega \setminus A \in \mathcal{S}$.

Một họ như vậy được gọi là một **đại số** các tập con của $\Omega$.

Trong trường hợp $\Omega$ là tập có vô hạn phần tử thì ta cần thêm điều kiện sau: nếu $A_i$, $i = 1, 2, 3, \ldots$ là một dãy vô hạn các phần tử của $\mathcal{S}$ thì hợp $\displaystyle{\bigcup_{i=1}^\infty A_i}$ cũng thuộc họ $\mathcal{S}$.

Với điều kiện thêm này, $\mathcal{S}$ được gọi là một **sigma-đại số**. Các phần tử của $\mathcal{S}$ được gọi là tập hợp con **đo được** của không gian xác suất.

2) Một hàm số thực $P : \mathcal{S} \to \mathbb{R}$, được gọi là **phân bố xác suất** hay **độ đo xác suất** trên $\Omega$, thỏa mãn các tính chất sau:

    i) với mọi $A \in \mathcal{S}$ ta có:

    $$0 \leqslant P(A) \leqslant 1$$

    ii)

    $$P(\emptyset) = 0, P(\Omega) = 1$$

    iii) nếu $A \cap B = \emptyset$ thì:

    $$P(A \cup B) = P(A) + P(B)$$

Tổng quát hơn, nếu $A_i$, với $i = 1, 2, 3, \ldots$ là một dãy các tập hợp con đo được và chúng đôi một không giao nhau thì:

$$P\left(\bigcup_i A_i\right) = \sum_{i} P(A_i)$$
````

Một số lưu ý:

1. Không gian xác suất $\Omega$ còn được gọi là **không gian mẫu** (hay **sample space**) và nó là mô hình toán học trừu tượng cho vấn đề tính toán xác suất đang được quan tâm. Mỗi phần tử của $\Omega$ có thể được gọi là một **sự kiện thành phần** (hay **biến cố sơ cấp**, **elementary event**). Nếu $A$ là một phần tử trong $\Omega$ thì ta cũng có thể viết $P(A)$ và hiểu là $P(\{ A \})$, trong đó $\{ A \}$ là tập con của $\Omega$ chứa duy nhất một phần tử $A$. Mỗi sự kiện là một tập con của $\Omega$ nên có thể chứa nhiều (thậm chí vô hạn) sự kiện thành phần. Không nhất thiết tập con nào của $\Omega$ cũng đo được (nằm trong họ $\mathcal{S}$) và chúng ta sẽ chỉ quan tâm đến các tập con đo được.
2. Trong toán học, một đại số là một tập hợp với các phép tính cộng, trừ và nhân (vành). Các tính chất của họ $\mathcal{S}$ trong định nghĩa không gian xác suất khiến nó là một đại số theo nghĩa:

    - phần tử $0$ trong $\mathcal{S}$ là tập rỗng
    - phần tử đơn vị trong $\mathcal{S}$ là tập $\Omega$
    - phép nhân trong $\mathcal{S}$ là phép giao $A \times B = A \cap B$
    - phép cộng trong $\mathcal{S}$ là phép $A + B = (A \cup B) \setminus (A \cap B) = (A \setminus B) \cup (B \setminus A)$

Đại số này có đặc số (số đặc trưng, characteristic) bằng $2$, tức là $2 A = A + A = 0$ với mọi $A$. Vì lý do này mà phép cộng và phép trừ là một. Chúng ta muốn $\mathcal{S}$ là một đại số để thuận tiện thực hiện tính toán số học.

3. Đẳng thức $P\left(\bigcup\limits_i A_i\right) = \sum\limits_{i} P(A_i)$ được gọi là **tính chất sigma** của xác suất. Tính chất sigma là **tính chất cộng vô hạn**: khi có một dãy vô hạn các tập con không giao nhau thì xác suất của hợp của chúng cũng bằng tổng vô hạn của các xác suất của các tập con. Tính chất sigma chính là tính chất cho phép chúng ta lấy giới hạn cho việc tính toán xác suất.

Ví dụ, nếu $A_1 \subset A_2 \subset \ldots$ là một dãy tăng các tập con của $\Omega$ và $A = \lim\limits_{n \to \infty} A_n = \bigcup\limits_{n=1}^\infty A_n$, thì ta có thể viết $P(A) = \lim\limits_{n \to \infty} P(A_n)$ bởi vì:

$$\begin{align*}
P(A) & = P(A_1 \cup \bigcup_{n=1}^\infty (A_{n+1} \setminus A_n)) = P(A_1) + \sum_{n=1}^\infty P(A_{n+1} \setminus A_n) \\
& = P(A_1) + \lim_{n \to \infty} P(A_{n+1} \setminus A_n) = P(A_1) + \lim_{n \to \infty}(P(A_{n+1}) - P(A_1))
\end{align*}$$

Đẳng thức $P\left(\bigcup\limits_i A_i\right) = \sum\limits_{i} P(A_i)$ không được suy ra từ $P(A \cup B) = P(A) + P(B)$ mà là một tiên đề trong xác suất. Tiên đề này được đưa ra bởi nhà toán học người Nga Andrei Nikolaievich Kolmogorov.

### Phép cộng xác suất mở rộng

Ở tiên đề 3 bên trên, hai biến cố khi đó được gọi là **xung khắc**, nghĩa là nếu biến cố này xảy ra thì biến cố kia chắc chắn không xảy ra. Nói cách khác giao của chúng bằng rỗng.

Ta còn có thể ký hiệu giao hai biến cố $P(A \cap B)$ là $P(AB)$.
    
Một trường hợp đơn giản nhất của hai biến cố xung khắc là **biến cố đối**.

````{prf:example}
Tung một đồng xu và gọi $A$ là biến cố đồng xu ra mặt ngửa. Khi đó biến cố đối của $A$, kí hiệu là $\bar{A}$ là biến cố ra mặt sấp. Ở đây $A \cup \bar{A} = \Omega$ và $A \cap \bar{A} = \emptyset$.

Từ đó:

$$1 = P(\Omega) = P(A \cup \bar{A}) = P(A) + P(\bar{A}),$$

nói cách khác $P(\bar{A}) = 1 - P(A)$.
````

Xét hai tập hợp $A$ và $B$. Số phần tử của phép hợp hai tập hợp trong trường hợp tổng quát được tính như sau: 

$$|A \cup B| = |A| + |B| - |A \cap B|$$
    
Tương tự, xác suất của phép cộng xác suất đối với hai biến cố có giao khác rỗng là: 

$$P(A \cup B) = P(A) + P(B) - P(A B)$$

Xét các tập hợp $A_1$, $A_2$, ..., $A_n$. Khi đó, số phần tử khi hợp các tập hợp này là:

$$\begin{equation*}
    \begin{split}
        |A_1 \cup A_2 \cup \cdots \cup A_n| & = |A_1| + |A_2| + \cdots + |A_n| - \sum_{i, j}|A_i \cap A_j| \\ & + \sum_{i, j, k} |A_i \cap A_j \cap A_k| + \cdots \\ & = \sum_{i=1}^n (-1)^{i+1} \sum_{j_1, j_2, \cdots, j_i} |A_{j_1} \cap A_{j_2} \cap \cdots \cap A_{j_i} |
    \end{split}
\end{equation*}$$

Tương tự, ta có phép cộng xác suất:

````{prf:theorem} Phép cộng xác suất mở rộng
$$   \begin{equation*}
    P(A_1 \cup A_2 \cup \cdots \cup A_n) = \sum_{i=1}^n (-1)^{i+1} \sum_{j_1, j_2, \cdots, j_i} P(A_{j_1} \cap A_{j_2} \cap \cdots \cap A_{j_i})
\end{equation*}$$
````

### Mô hình xác suất với vô hạn các sự kiện

````{prf:example} Phân phối Poisson
Giả sử tỉ lệ số khách hàng trung bình đến siêu thị trong một đơn vị thời gian cố định là $\lambda$. Phân phối Poisson $P(n) = e^{-\lambda} \cdot \dfrac{\lambda^n}{n!}$ thể hiện xác suất có $n$ khách hàng đến siêu thị theo tỉ lệ thời gian $\lambda$. 
````

Ở phân phối Poisson, $n$ nhận tất cả giá trị nguyên không âm $0, 1, \ldots$ cũng như thỏa điều kiện:

$$\sum_{n=0}^{\infty} P(n) = \sum_{n=0}^\infty e^{-\lambda} \cdot \frac{\lambda^n}{n!} = e^{-\lambda} \sum_{n=0}^\infty \frac{\lambda^n}{n!} = e^{-\lambda} \cdot e^\lambda = 1.$$

Ở biến đổi trên, $\displaystyle{\sum_{n=0}^\infty \frac{\lambda^n}{n!} = e^\lambda}$ là khai triển Taylor.

````{prf:example}
Giả sử ta biết rằng có một xe hơi $X$ đang đậu trên một khúc phố $Z$ và ta quan tâm đến vị trí của $X$ trên khúc phố đó. Ta có thể mô hình $X$ bằng một điểm và $Z$ là một đoạn thẳng và lấy đoạn thẳng đó làm không gian xác suất $\Omega = [a, b]$, $a, b \in \mathbb{R}, a < b$. (mô hình xác suất liên tục này có lực lượng continuum, không đếm được). Sự kiện "xe hơi đỗ chỗ nào đó trên khúc phố" chuyển thành sự kiện "điểm $x$ nằm trong một đoạn thẳng con nào đó trên đoạn thẳng $\Omega = [a, b]$". Ta có thể chọn phân bố xác suất đều trên $\Omega = [a, b]$ theo nghĩa sau: xác suất mỗi đoạn thẳng con trên $\Omega$ tỷ lệ thuận với độ dài của đoạn thẳng con đó, hay $P([c, d]) = (d - c) / (b - a)$.
````

### Ánh xạ giữa các không gian xác suất

````{prf:definition} Ánh xạ bảo toàn xác suất
Một ánh xạ $\phi : (\Omega_1, P_1) \to (\Omega_2, P_2)$ từ một không gian xác suất $(\Omega_1, P_1)$ vào một không gian xác suất $(\Omega_2, P_2)$ được gọi là một **ánh xạ bảo toàn xác suất** nếu nó bảo toàn độ đo xác suất, nghĩa là với mọi tập con $B \subset \Omega_2$ đo được, ta có:

$$P_1(\phi^{-1}(B)) = P_2(B)$$
````

Hơn nữa, nếu $\phi$ là một song ánh modulo những tập có xác suất bằng $0$, nghĩa là tồn tại các tập con $A \in \Omega_1$, $B \in \Omega_2$ sao cho $P_1(A) = P_2(B) = 0$ và $\phi : \Omega_1 \setminus A \to \Omega_2 \setminus B$ là song ánh bảo toàn xác suất, thì $\phi$ được gọi là **đẳng cấu xác suất**, và ta nói rằng $(\Omega_1, P_1)$ đẳng cấu xác suất với $(\Omega_2, P_2)$.

````{prf:theorem}
Nếu $(\Omega_1, P_1)$ là một không gian xác suất và $\phi : \Omega_1 \to \Omega_2$ là một ánh xạ tùy ý thì tồn tại một độ đo xác suất $P_2$ sao cho ánh xạ $\phi : (\Omega_1, P_1) \to (\Omega_2, P_2)$ là ánh xạ bảo toàn xác suất.
````

Ta xây dựng $P_2$ theo công thức: với mỗi tập con $B \subset \Omega_2$, nếu tồn tại $P_1(\phi^{-1}(B))$ thì ta đặt

$$P_2(B) = P_1(\phi^{-1}(B))$$

Độ đo xác suất $P_2$ như trên gọi là **push-forward** của $P_1$ qua ánh xạ $\phi$, hay **phân bố xác suất cảm sinh** từ $P_1$ qua ánh xạ $\phi$.

**Câu hỏi:** chứng minh rằng quan hệ đẳng cấu xác suất giữa các không gian xác suất là một quan hệ tương đương.

Giải: vì $\phi$ là song ánh, đối với tính phản xạ chúng ta lấy ánh xạ đồng nhất, tính đối xứng thì ánh xạ ngược của song ánh (vẫn là song ánh), bắc cầu thì ta hợp hai song ánh vẫn là song ánh.

### Tích của các không gian xác suất

Nếu $(\Omega_1, P_1)$ và $(\Omega_2, P_2)$ là hai không gian xác suất thì tích $\Omega_1 \times \Omega_2$ cũng có một độ đo xác suất $P$ được xác định bởi $P_1$ và $P_2$ bằng công thức: nếu $A_1 \subset \Omega_1$ và $A_2 \subset \Omega_2$ nằm trong các sigma-đại số tương ứng của $P_1$ và $P_2$ thì:

$$P(A_1 \times A_2) = P_1(A_1) \times P_2(A_2).$$

Sigma-đại số của $P$ chính là sigma-đại số sinh bởi các tập con của $\Omega_1 \times \Omega_2$ có dạng $A_1 \times A_2$ như trên.

Tương tự ta có thể định nghĩa tích trực tiếp của $n$ không gian xác suất hay thập chí một dãy vô hạn các không gian xác suất.

````{prf:theorem}
Hai phép chiếu tự nhiên từ tích $(\Omega_1, P_1) \times (\Omega_2, P_2)$ của hai không gian xác suất xuống $(\Omega_1, P_1)$ và $(\Omega_2, P_2)$ là hai ánh xạ bảo toàn xác suất.
````

## Xác suất có điều kiện

### Xác suất có điều kiện

````{prf:definition} Xác suất có điều kiện
Xét hai biến cố $A$ và $B$. Khi đó xác suất xảy ra của biến cố $B$ với điều kiện biến cố $A$ xảy ra là: 

$$\begin{equation}
    P(A \vert B) = \frac{P(AB)}{P(B)}
\end{equation}$$
````

Ý nghĩa của công thức trên có thể hiểu là, việc biến cố $A$ xảy ra dựa trên cơ sở biến cố $B$ đã xảy ra, do đó không gian mẫu sẽ giảm xuống còn $B$ và biến cố giảm còn $AB$.

Dựa trên định nghĩa của xác suất có điều kiện có thể đưa ra nhận xét sau.

````{prf:remark}
Từ công thức trên có thể thấy sự tương đương:

$$\begin{equation*}
    P(AB) = P(B) \cdot P(A \vert B) = P(A) \cdot P(B \vert A)
\end{equation*}$$
````

Nhận xét trên cho thấy sự liên hệ của hai biến cố. Nói cách khác việc xảy ra của biến cố này sẽ ảnh hưởng đến biến cố kia và ngược lại.

Tổng quát, nếu $n$ biến cố $A_i$, $i=1, \ldots, n$ không độc lập thì:

$$\begin{align*}
    P(A_1 A_2 \cdots A_n) = & P(A_1) \cdot P(A_2 | A_1) \cdot P(A_3 | A_2 A_1) \cdots \\ & P(A_n|A_1A_2 \cdots A_{n-1})
\end{align*}$$

Sử dụng nhận xét trên có thể chứng minh công thức này bằng quy nạp. Về mặt ý nghĩa, biến cố $A_1$ xảy ra đầu tiên. Tiếp theo đó $A_2$ xảy ra với điều kiện $A_1$ đã xảy ra. Tiếp theo nữa, $A_3$ xảy ra khi cả $A_1$ và $A_2$ xảy ra, chính là $A_1 A_2$.

Tương tự như vậy, $A_i$ xảy ra với điều kiện tất cả $A_1, \ldots, A_{i-1}$ đều đã xảy ra, là biến cố giao $A_1 \ldots A_{i_1}$.

Cũng từ nhận xét trên, các biến cố có vai trò như nhau nên việc đổi vị trí không thay đổi kết quả $P(A_1 \ldots A_n)$.

### Sự độc lập và phụ thuộc của các sự kiện

Nếu hai biến cố không ảnh hưởng việc xảy ra của nhau thì ta gọi là biến cố độc lập.

````{prf:definition} Biến cố độc lập
Hai biến cố được gọi là **độc lập** nếu việc xảy ra của biến cố này không ảnh hưởng đến việc xảy ra của biến cố kia, hay:

$$P(A) = P(A \vert B) = P(AB) / P(B)$$
````

Viết cách khác là:

$$P(AB) = P(A) \cdot P(B)$$

Khi đó, giả sử ta có một họ $\mathcal{M}$ các sự kiện.

````{prf:definition} Họ các sự kiện độc lập
Họ $\mathcal{M}$ được gọi là một **họ các sự kiện độc lập** nếu như với bất kì số tự nhiên $k$ nào và bất kì sự kiện $A_i, \ldots, A_k$ khác nhau nào trong họ $\mathcal{M}$ ta cũng có:

$$P(A_1 \cdots A_k) = P(A_1) \cdot P(A_2) \cdots P(A_k).$$
````

````{prf:remark}
Nếu ta có một họ các sự kiện độc lập thì các sự kiện trong họ độc lập đôi một với nhau. Nhưng ngược lại chưa chắc: có những họ không độc lập mà trong đó các sự kiện độc lập từng đôi một với nhau!
````

### Công thức xác suất toàn phần

````{prf:definition} Hệ biến cố đầy đủ
Xét phép thử có không gian mẫu là $\Omega$. Một hệ các biến cố $A_1$, $A_2$, ..., $A_n$ là một **hệ biến cố đầy đủ** (hoặc **phân hoạch**) của $\Omega$ nếu chúng thỏa các điều kiện:

- $A_1 \cup A_2 \cup \cdots \cup A_n = \Omega$
- $A_i \cap A_j = \emptyset$ với mọi $i \neq j$
````

````{prf:example}
Một hệ biến cố đầy đủ đơn giản là $\Omega = \{ A, \bar{A} \}$ gồm biến cố $A$ và biến cố đối của $A$.
````

Khi có một hệ biến cố đầy đủ, ta có thể tính xác suất của một biến cố bất kì nếu biết xác suất của các biến cố trong hệ biến cố đầy đủ và xác suất có điều kiện tương ứng.

````{prf:theorem} Công thức xác suất toàn phần
Gọi $A_1, A_2, \ldots, A_n$ là một hệ biến cố đầy đủ của $\Omega$. Khi đó, với biến cố $B$ bất kì trong phép thử: 

$$\begin{equation}    
    P(B) = P(A_1) \cdot P(B | A_1) + \cdots + P(A_n) \cdot P(B | A_n)
\end{equation}$$
````

````{prf:example}
**Đề bài.** Trong một lớp học có 15 bạn nam và 10 bạn nữ. Trong đó có 5 bạn nam biết chơi bóng chuyền và 2 bạn nữ biết chơi bóng chuyền. Chọn ngẫu nhiên một bạn trong lớp, tính xác suất bạn đó biết chơi bóng chuyền.

**Giải.** Bài này có thể giải đơn giản bằng việc xác định số bạn biết chơi bóng chuyền là $5 + 2 = 7$ (5 nam và 2 nữ), trong khi không gian mẫu là $15 + 10 = 25$ nên kết quả là $\dfrac{7}{25}$.

Bài này nhằm đưa ra cái nhìn đơn giản về việc xác định điều kiện để thành lập hệ biến cố đầy đủ và giải bài toán. 

Ở đây chúng ta cần tìm một hệ biến cố đầy đủ. Gọi $A_1$ là biến cố bạn được chọn là nam và $A_2$ là biến cố bạn được chọn là nữ. Như vậy $\Omega = \{ A_1, A_2 \}$ thỏa định nghĩa về hệ biến cố đầy đủ. Dễ thấy $P(A_1) = \dfrac{15}{25} = \dfrac{3}{5}$ và $P(A_2) = \dfrac{10}{25} = \dfrac{2}{5}$.

Tiếp theo, gọi $B$ là biến cố bạn được chọn biết chơi bóng chuyền.

Khi đó, xác suất một bạn biết chơi bóng chuyền với điều kiện bạn đó là nam bằng $P(B \vert A_1) = \dfrac{5}{15} = \dfrac{1}{3}$.

Tương tự, xác suất một bạn biết chơi bóng chuyền với điều kiện bạn đó là nữ bằng $P(B \vert A_2) = \dfrac{2}{10} = \dfrac{1}{5}$.

Theo công thức xác suất toàn phần, xác suất bạn được chọn ngẫu nhiên biết chơi bóng chuyền là $P(B)$ và ta tính được

$$\begin{equation*}
    P(B) = P(A_1) \cdot P(B \vert A_1) + P(A_2) \cdot P(B \vert A_2) = \frac{3}{5} \cdot \frac{1}{3} + \frac{2}{5} \cdot \frac{1}{5} = \frac{7}{25}.
\end{equation*}$$
````

Ở đây, nếu chúng ta đảo điều kiện đề bài, ví dụ như bạn được chọn ngẫu nhiên là nữ *với điều kiện bạn đó biết chơi bóng chuyền* thì sao? Đề bài lúc này tương đương việc tính $P(A_2 \vert B)$.

Để trả lời câu hỏi này chúng ta sử dụng công thức Bayes.

### Công thức Bayes

````{prf:theorem} Công thức Bayes
Xét hệ biến cố đầy đủ $\{ A_1, A_2, \ldots, A_n \}$ của không gian xác suất. Với biến cố $B$ bất kì ta có **công thức Bayes**: 

$$P(A_i | B) = \frac{P(A_i) P(B | A_i)}{\displaystyle{\sum_{j=1}^n P(A_j) P(B | A_j)}}$$

với mọi $1 \leqslant i \leqslant n$.
````

Công thức Bayes thực ra là công thức xác suất có điều kiện $P(B) \cdot P(A \vert B) = P(A) \cdot P(B \vert A)$, trong đó ta thay $P(B)$ bởi công thức xác suất toàn phần.

Như vậy, để trả lời cho câu hỏi trên, ta có

$$\begin{equation*}
    P(A_2 \vert B) = \dfrac{P(A_2) \cdot P(B \vert A_2)}{P(B)} = \dfrac{\dfrac{2}{5} \cdot \dfrac{1}{5}}{\dfrac{7}{25}} = \dfrac{2}{7}.
\end{equation*}$$

## Biến ngẫu nhiên

### Biến ngẫu nhiên

Xét phép thử với không gian mẫu $\Omega$. Với mỗi biến cố sơ cấp $\omega \in \Omega$ ta liên kết với một số thực $\xi(\omega) \in \mathbb{R}$ thì $\xi$ được gọi là **biến ngẫu nhiên** (hay **random variable**, BNN).

````{prf:definition} Biến ngẫu nhiên
**Biến ngẫu nhiên** $\xi$ của một phép thử với không gian mẫu $\Omega$ là ánh xạ: 

$$\begin{equation*}
    \begin{split}
        \xi = \xi (\omega), \quad \omega \in \Omega
    \end{split}
\end{equation*}$$
````

Giá trị $\xi(\omega)$ được gọi là một giá trị của biến ngẫu nhiên $\xi$.

- Nếu $\xi(\Omega)$ là một tập hữu hạn $\{\xi_1, \xi_2, \ldots,\xi_n\}$ hay tập vô hạn đếm được thì $\xi$ được gọi là **biến ngẫu nhiên rời rạc**.
- Nếu $\xi(\Omega)$ là một khoảng của $\mathbb{R}$ hay toàn bộ $\mathbb{R}$ thì $\xi$ được gọi là **biến ngẫu nhiên liên tục**.

### Phân bố xác suất của biến ngẫu nhiên

````{prf:definition} Hàm phân phối xác suất
**Hàm phân phối** của biến ngẫu nhiên $\xi$ là hàm số $F(x)$, xác định bởi:

$$\begin{equation}
    F(x) = P(\xi \leqslant x), \quad x \in \mathbb{R}
\end{equation}$$
````

Ở đây ta viết gọn $P(\xi \leqslant x)$ từ $P(\{ \omega: \xi(\omega) \leqslant x \})$. Tập hợp $\{ \omega: \xi(\omega) \leqslant x\}$ có thể không thuộc một biến cố nào, do đó có thể là tập rỗng (ứng với xác suất là $0$).

### Tính chất của hàm phân phối

**Tính chất 1.** Hàm phân phối $F(x)$ không giảm trên mọi đoạn thẳng.

```{admonition} **Chứng minh.**
:class: danger, dropdown
Đặt $x_2 > x_1$. Ta thấy rằng

$$\{ \xi \leqslant x_2 \} = \{ \xi \leqslant x_1 \} + \{ x_1 < \xi \leqslant x_2 \},$$

Do đó nếu ta lấy xác suất thì cũng có

$$P(\xi \leqslant x_2) = P(\xi \leqslant x_1) + P(x_1 < \xi \leqslant x_2)$$

Xác suất luôn không âm, hay $P(x_1 < \xi \leqslant x_2) \geqslant 0$, suy ra $P(\xi \leqslant x_2) \geqslant P(\xi \leqslant x_1)$, hay $F(x_2) \geqslant F(x_1)$.
````

**Tính chất 2.** $\displaystyle{\lim_{x \to -\infty} F(x) = 0}$.

**Tính chất 3.** $\displaystyle{\lim_{x \to +\infty} F(x) = 1}$.

**Tính chất 4.** Hàm phân phối $F(x)$ liên tục phải trên toàn trục số.

Để chứng minh các tính chất 2, 3, 4 chúng ta cần các tiên đề của sự liên tục (continunity axioms) và sẽ không đề cập ở đây.

### Biến ngẫu nhiên rời rạc

Cho BNN rời rạc $\xi = \xi(\omega)$, $\xi = \{ a_1, a_2, \ldots, a_n, \ldots \}$. Giả sử $a_1 < a_2 < \ldots < a_n < \ldots$ với xác suất tương ứng là $P(\xi = a_i) = p_i$, $i = 1, 2, \ldots$

Ta có thể biểu diễn biến ngẫu nhiên và xác suất tương ứng của nó bằng bảng phân phối xác suất của $\xi$.

| $\xi$ | $a_1$ | $a_2$ | $\cdots$ | $a_n$ | $\cdots$ |
| :---: | :---: | :---: | :------: | :---: | :------: |
| $P$ | $p_1$ | $p_2$ | $\cdots$ | $p_n$ | $\cdots$ |

Rõ ràng rằng $p_n \geqslant 0$ với mọi $n$. Hơn nữa:

$$\sum_{n=1}^\infty p_n = 1$$

Không gian mẫu lúc này là hợp của các tập biến ngẫu nhiên rời rạc:

$$\Omega = \{ \xi = a_1 \} \cup \{ \xi = a_2 \} \cup \ldots$$

Các biến ngẫu nhiên xung khắc nhau (vì $\xi$ không thể nhận hai giá trị khác nhau cùng lúc), do đó xác suất cả không gian mẫu là

$$1 = P(\Omega) = P(\xi = a_1) + P(\xi = a_2) + \ldots = p_1 + p_2 + \ldots$$

````{prf:definition} Phân bố Bernoulli
Phân bố xác suất cho không gian sinh bởi đúng một sự kiện $A$ và phủ định của nó $\bar{A}$, hay $\Omega = \{ A, \bar{A} \}$. Nếu xác suất xảy ra sự kiện $A$ là $p$ thì xác suất xảy ra $\bar{A}$ là $1-p$.
````

Phân bố Bernoulli được đặt tên theo nhà toán học Jacob Bernoulli (1654-1705).

````{prf:definition} Phân phối nhị thức
Biến ngẫu nhiên $\xi$ được gọi là có **phân phối nhị thức** với tham số $p$, $n$, với $p \in [0, 1]$ và $n$ là số tự nhiên, nếu $\xi$ nhận các giá trị $0, 1, \ldots, n$ và

$$\begin{equation}
    P(\xi = k) = C^k_n p^k q^{n-k}, \quad k = 0, 1, \ldots, n
\end{equation}$$

Ở đây $q = 1 - p$.
````

````{prf:example}
Một bài kiểm tra có 100 câu hỏi trắc nghiệm bốn đáp án. Xác suất chọn ngẫu nhiên đúng đáp án của mỗi câu hỏi thì giống nhau và bằng $\dfrac{1}{4}$.

Ở đây xác suất chọn ngẫu nhiên đúng đáp án của một câu hỏi bất kì là $p = \dfrac{1}{4}$, và số lượng câu hỏi là $n = 100$.

Gọi $\xi$ là biến ngẫu nhiên số câu hỏi trả lời đúng. Khi đó $\xi$ nhận các giá trị $0, 1, \ldots, 100$.

Do đó bài toán này có phân phối nhị nhức và

$$P(\xi = k) = C^k_{100} \left(\dfrac{1}{4}\right)^k \left(\dfrac{3}{4}\right)^{100-k}$$ 
````

````{prf:definition} Phân bố xác suất đều
Phân bố xác suất $P$ trên không gian xác suất hữu hạn với $N$ phần tử $\Omega = \{ A_1, \ldots, A_n \}$ được gọi là **phân bố xác suất đều** nếu như $P(A_1) = \ldots = P(A_n) = 1 / N$.
````

Khái niệm phân bố đều không mở rộng được lên các không gian xác suất có số phần tử là vô hạn và đếm được vì $1$ chia vô cùng bằng $0$ mà tổng của chuỗi vô hạn số $0$ vẫn bằng $0$ chứ không bằng $1$.

````{prf:remark}
Phân bố xác suất đều có **tính đối xứng**, **cân bằng** hay **hoán vị được** của các sự kiện thành phần.
````

````{prf:definition} Phân phối Poisson
Biến ngẫu nhiên $\xi$ được gọi là có **phân phối Poisson** với tham số $\lambda$, nếu $\xi$ nhận các giá trị $0, 1, \ldots, n$ và 

$$\begin{equation}
    P(\xi = k) = \dfrac{\lambda^k \cdot e^{-\lambda}}{k!}, \quad k = 0, 1, \ldots, n
\end{equation}$$
````

Tham số $\lambda$ thể hiện số lần trung bình mà một sự kiện xảy ra trong một khoảng thời gian nhất định. Khi đó, nếu một biến ngẫu nhiên có số lần xuất hiện trung bình của một sự kiện trong thời gian $t$ thì nó có phân phối Poisson với tham số $\lambda t$, với $\lambda$ là số lần trung bình trong một đơn vị thời gian.

### Biến ngẫu nhiên liên tục

````{prf:definition} Biến ngẫu nhiên liên tục
Biến ngẫu nhiên $\xi$ được gọi là **liên tục**, nếu nó nhận giá trị tại mọi điểm thuộc một đoạn liên tục nào đó trên trục số, và tồn tại một hàm số không âm $p(x)$ sao cho với mọi đoạn $[a ,b]$ (hữu hạn hoặc vô hạn) ta có

$$\begin{equation}
    P(a \leqslant \xi \leqslant b) = \int\limits_{a}^{b} p(x)\, dx
\end{equation}$$

Hàm $p(x)$ được gọi là **hàm mật độ** của biến ngẫu nhiên $\xi$.
````

Tương tự biến ngẫu nhiên rời rạc, $p(x) \geqslant 0$ với mọi $x \in \mathbb{R}$ và khi hai cận là vô cực thì biến ngẫu nhiên bao quát toàn bộ không gian mẫu. Nghĩa là

$$\int\limits_{-\infty}^{+\infty} p(x)\, dx = 1$$

Từ định nghĩa của hàm phân phối $F(x) = P(\xi \leqslant x)$ ta có hai tính chất của hàm mật độ:

1. $\displaystyle{F(x) = \int\limits_{-\infty}^{x} p(x)\, dx}$.
2. $p(x) = F'(x)$.

Tính chất thứ nhất là từ định nghĩa hàm phân phối. Tính chất thứ hai suy ra từ việc cận trên của tích phân là hữu hạn.

### Hàm mật độ của biến ngẫu nhiên rời rạc

Biến ngẫu nhiên rời rạc có bảng xác suất sau:

| $x$ | $x_1$ | $x_2$ | $\cdots$ | $x_n$ | $\cdots$ |
| :---: | :---: | :---: | :------: | :---: | :------: |
| $P$ | $p_1$ | $p_2$ | $\cdots$ | $p_n$ | $\cdots$ |

Khi đó hàm mật độ của $X$ là:

$$f(x) = \begin{cases}
        p_i & \text{khi} \ x = x_i, \\
        0 & \text{khi} \ x \neq x_i, \ \text{với mọi} \ i
\end{cases}$$

````{prf:remark}
Ta có các lưu ý sau:
- $p_i \geqslant 0$, $\sum p_i = 1$, $i = 1, 2, \ldots$
- $\displaystyle{P(a < X \leqslant b) = \sum_{a < x_i \leqslant b} p_i}$
````

### Hàm mật độ của biến ngẫu nhiên liên tục

````{prf:definition}
Hàm số $f: \mathbb{R} \mapsto \mathbb{R}$ được gọi là **hàm mật độ** của biến ngẫu nhiên liên tục $X$ nếu:

$$P(a \leqslant X \leqslant b) = \displaystyle{\int\limits_a^b f(x)\,dx}, \forall a, b \in \mathbb{R}$$
````

````{prf:remark}
Với mọi $x \in \mathbb{R}$, $f(x) \geqslant 0$ và $\displaystyle{\int\limits_{-\infty}^{+\infty}f(x)\,dx = 1}$.
````

**Ý nghĩa hình học.** Xác suất của biến ngẫu nhiên $X$ nhận giá trị trong $[a, b]$ bằng diện tích hình thang cong giới hạn bởi $x=a$, $x=b$, $y=f(x)$ và $Ox$.


