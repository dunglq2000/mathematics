## Nhóm

```{contents}
```

### Nhóm và nhóm con

````{prf:definition} Nhóm
Một tập hợp $G$ và toán tử hai ngôi $\star$ trên $G$ tạo thành một **nhóm** (hay **group**, **группа**) nếu:

1. Tồn tại phần tử $e \in G$ sao cho với mọi $g \in G$ thì $g \star e = e \star g = g$. Khi đó $e$ được gọi là **phần tử đơn vị** của $G$;
2. Với mọi $g \in G$, tồn tại $g' \in G$ sao cho $g \star g' = g' \star g = e$. Khi đó $g'$ được gọi là **phần tử nghịch đảo** của $g$;
3. Tính kết hợp: với mọi $a, b, c \in G$ thì $a \star (b \star c) = (a \star b) \star c$.
````

````{prf:definition} Nhóm Abel
Nếu nhóm $G$ có thêm tính giao hoán, tức là với mọi $a, b \in G$ thì $a \star b = b \star a$ thì $G$ gọi là **nhóm giao hoán** hoặc **nhóm Abel** (**abelian group**, **commutative group**, **абелева группа**, **коммутативная группа**).
````

````{prf:example}
Xét tập hợp số nguyên $\mathbb{Z}$ và phép cộng hai số nguyên.
1. Phần tử đơn vị là 0 vì với mọi $a \in \mathbb{Z}$ thì $a + 0 = 0 + a = a$;
2. Với mọi $a \in \mathbb{Z}$, phần tử nghịch đảo là $-a$ vì $a + (-a) = (-a) + a = 0$;
3. Phép cộng số nguyên có tính kết hợp do đó thỏa mãn điều kiện về tính kết hợp.

Như vậy $(\mathbb{Z}, +)$ tạo thành nhóm. Lưu ý do phép cộng hai số nguyên có tính giao hoán nên đây cũng là nhóm Abel.
````

````{prf:example}
Xét tập hợp số hữu tỉ khác 0 $\mathbb{Q}^*$ và phép nhân hai số hữu tỉ. Ta thấy do $a, b \in \mathbb{Q}^*$ nên tích $a \cdot b$ cũng khác 0, do đó cũng thuộc $\mathbb{Q}^*$.

1. Phần tử đơn vị là 1 vì với mọi $a \in \mathbb{Q}^*$ thì $a \cdot 1 = 1 \cdot a = a$;
2. Với mọi $a \in \mathbb{Q}^*$, phần tử nghịch đảo là $\dfrac{1}{a}$ vì $a \cdot \dfrac{1}{a} = \dfrac{1}{a} \cdot a = 1$;
3. Phép nhân hai số hữu tỉ có tính kết hợp do đó thỏa mãn điều kiện về tính kết hợp.

Tương tự như nhóm $(\mathbb{Z, +})$, nhóm $(\mathbb{Q}^*, \cdot)$ cũng là nhóm Abel.
````

````{prf:definition} Order của nhóm
**Order** (hay **порядок**) của nhóm $G$ là lực lượng (hay số phần tử, **carninality**) của nhóm đó và ký hiệu là $\lvert G \rvert$.
````

Đối với nhóm có vô hạn phần tử, ta quy ước order của nhóm bằng $0$, ví dụ như với hai nhóm $(\mathbb{Z}, +)$ và $(\mathbb{Q}^*, \cdot)$ ở trên.

### Nhóm con

````{prf:definition} Nhóm con
Cho nhóm $(G, \star)$. Tập hợp $H \subset G$ được gọi là **nhóm con** (hay **subgroup**, **подгруппа**) của $G$ nếu với mọi $a, b \in H$ thì $a \star b \in H$
````
 
Nghĩa là toán tử $\star$ đóng với các phần tử trong $H$.

````{prf:example}
Xét nhóm $(\mathbb{Z}, +)$ như trên. Ta xét tập con gồm các số chẵn của nó

$$2\mathbb{Z} = \{ \ldots, -4, -2, 0, 2, 4, \ldots \}$$

Ta thấy rằng tổng hai số chẵn vẫn là số chẵn, nghĩa là phép cộng số nguyên đóng trên $2\mathbb{Z}$.

Do đó $(2\mathbb{Z}, +)$ là nhóm con của $(\mathbb{Z}, +)$.

Tổng quát, mọi tập hợp có dạng $n \mathbb{Z}$ đều là nhóm con của $(\mathbb{Z}, +)$.
````

````{prf:theorem} Định lý Lagrange
Order của nhóm luôn chia hết order của một nhóm con bất kì của nó.
````

### Nhóm vòng

````{prf:definition} Nhóm vòng
Nhóm $G$ được gọi là **nhóm vòng** (hay **cyclic group**, **циклическая группа**) nếu tồn tại phần tử $g \in G$ mà mọi phần tử trong $G$ đều được biểu diễn dưới dạng $g^i$. Khi đó ta kí hiệu $G = \langle g \rangle$ hoặc $G = \{ g, g^1, \ldots, g^n \}$.
````

Thông thường ta quy ước $g^n = g^0 = e$.

Đối với nhóm $(\mathbb{Z}_n, +_n)$ xác định phép cộng modulo $n$, ta kí hiệu $ig = \underbrace{g + g + \ldots + g}_{i \,\text{lần}}$.

Ta viết $G = \{ 1g, 2g, 3g, \ldots, ng \}$. Phần tử $g$ được gọi là **phần tử sinh** (hay **образующий элемент**) của nhóm vòng $G$.

Như vậy, số lượng phần tử sinh của $\mathbb{Z}_n$ là $\varphi(n)$ với $\varphi$ là hàm Euler. Lúc này điều kiện để phần tử $j$ là phần tử sinh tương đương với $\langle j \rangle = \mathbb{Z}_n \Longleftrightarrow (j, n) = 1$.

````{prf:definition} Elementary abelian group
Nhóm vòng được gọi là **elementary abelian** (hay **примарная абелева группа**) nếu bậc của nhóm là số nguyên tố.
````

### Coset

````{prf:definition} Coset, lớp kề
Cho nhóm $G$ và nhóm con $H$ của $G$.

Coset trái của $H$ đối với phần tử $g \in G$ là tập hợp

$$gH = \{gh : h \in H \}$$

Tương tự, coset phải là tập hợp

$$Hg = \{hg : h \in H \}$$
````

Từ đây nếu không nói gì thêm ta ngầm hiểu là coset trái.

Ví dụ với nhóm con $2\mathbb{Z}$ của $\mathbb{Z}$, ta thấy rằng

1. Nếu $g \in \mathbb{Z}$ là lẻ thì khi cộng với bất kì phần tử nào của $2\mathbb{Z}$ ta có số lẻ;
2. Nếu $g \in \mathbb{Z}$ là chẵn thì khi cộng với bất kì phần tử nào của $2\mathbb{Z}$ ta có số chẵn.

Nói cách khác, coset của $2\mathbb{Z}$ chia tập $\mathbb{Z}$ thành

$$0 + 2\mathbb{Z} = \{\ldots, -4, -2, 0, 2, 4, \ldots\}$$
 
$$1 + 2\mathbb{Z} = \{\ldots, -3, -1, 1, 3, \ldots \}$$

Rõ ràng hai coset trên rời nhau.

````{prf:remark}
Hai coset bất kì hoặc rời nhau, hoặc trùng nhau.
````

```{admonition} **Chứng minh**
:class: danger, dropdown
Nếu hai coset rời nhau thì không có gì phải nói. Ta chứng minh trường hợp còn lại.

Giả sử $g_1 H \cap g_2 H \neq \emptyset$. Như vậy tồn tại $h_1, h_2 \in H$ mà $g_1 h_1 = g_2 h_2$.

Do $h_1^{-1} \in H$, ta có $g_1 = g_2 h_2 h_1^{-1}$, nghĩa là $g_1 \in g_2 H$.

Mà mọi phần tử trong $g_1 H$ có dạng $g_1 h$ nên $g_1 h = g_2 h_2 h_1^{-1} h$. Do $H$ là nhóm con của $G$ nên $h_2 h_1^{-1} h \in H$.

Từ đó $g_1 H \subseteq g_2 H$. Tương tự ta cũng có $g_2 H \subseteq g_1 H$. Vậy $g_1 H = g_2 H$.
```

### Normal Subgroup

````{prf:definition} Normal Subgroup
Nhóm con $H$ của $G$ được gọi là **normal subgroup** (hay **нормальная подгруппа**, **nhóm con chuẩn tắc**) nếu với mọi $g \in G$ ta có coset trái trùng với coset phải.

$$\begin{equation*}
    gH = Hg \quad \text{ với mọi } g \in G
\end{equation*}$$
````

Nếu $H$ là normal subgroup của $G$ ta ký hiệu $H \triangleleft G$. Khi đó, với mọi $a, b \in G$ thì $(a H) (b H) = (ab) H$.

````{prf:definition} Quotient Group
Với nhóm $G$ và normal subgroup của nó là $H$.

**Quotient Group** (hay **nhóm thương**) được ký hiệu là $G / H$ và được định nghĩa là tập hợp các coset tương ứng với normal subgroup $H$.

$$G / H = \{gH : g \in H \}$$

Ta thấy rằng điều này chỉ xảy ra nếu $H$ là normal subgroup.
````

Quotient Group còn được gọi là **Factor Group** (hay **nhóm nhân tử**).

````{prf:example}
Với nhóm $\mathbb{Z}$ và normal subgroup của nó là $2\mathbb{Z}$.
Ta thấy $\mathbb{Z} / 2 \mathbb{Z} = \{0 + 2 \mathbb{Z}, 1 + 2 \mathbb{Z}\}$
````

### Direct sum of modules

> Прямая сумма

Có hai dạng tổng là external và internal.

````{prf:definition} External direct sum
Giả sử ta có các nhóm $(G_1, *)$, $(G_2, \star)$, ..., $(G_t, \circ)$. Khi đó externel direct sum của các nhóm $G_1, \ldots, G_t$ là:

$$\begin{equation*}
    G = G_1 \times G_2 \times G_t, \quad (G, \square).
\end{equation*}$$
````

Giả sử $g = (g_1, g_2, \ldots, g_t) \in G$ với $g_i \in G_i$, và $g' = (g'_1, g'_2, \ldots, g'_t) \in G$ với $g'_i \in G_i$. Khi đó:

$$\begin{equation*}
    g \square g' = (g_1 * g'_1, g_2 \star g'_2, \ldots, g_t \circ g'_t).
\end{equation*}$$

````{prf:definition} Internal direct sum
Giả sử ta có nhóm $(G, \circ)$ và các nhóm con $G_1, G_2, \ldots, G_t$ của $G$. Khi đó internal direct sum là:

1. Với mọi $g \in G$ thì $g = g_1 \circ g_2 \circ \ldots \circ g_t$ với $g_i \in G_i$.
2. Với mọi $i, j$ mà $i \neq j$, $1 \leqslant i, j \leqslant t$ ta có

$$g_i \circ g_j = g_j \circ g_i$$

với mọi $g_i \in G_i$ và $g_j \in G_j$.
````