## Nhóm

```{contents}
```

### Nhóm và nhóm con

````{prf:definition} Group, Nhóm
Một tập hợp $G$ và toán tử hai ngôi $\star$ trên $G$ tạo thành một **nhóm** nếu:

1. Tồn tại phần tử $e \in G$ sao cho với mọi $g \in G$ thì $g \star e = e \star g = g$. Khi đó $e$ được gọi là **phần tử đơn vị** của $G$;
2. Với mọi $g \in G$, tồn tại $g' \in G$ sao cho $g \star g' = g' \star g = e$. Khi đó $g'$ được gọi là **phần tử nghịch đảo** của $g$;
3. Tính kết hợp: với mọi $a, b, c \in G$ thì $a \star (b \star c) = (a \star b) \star c$.
````

````{prf:definition} Abelian Group, Nhóm Abel
Nếu nhóm $G$ có thêm tính giao hoán, tức là với mọi $a, b \in G$ thì $a \star b = b \star a$ thì $G$ gọi là **nhóm giao hoán** hay **nhóm Abel**.
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

### Nhóm con

````{prf:definition} Subgroup, Nhóm con
Cho nhóm $(G, \star)$. Tập hợp $H \subset G$ được gọi là **nhóm con** của $G$ nếu với mọi $a, b \in H$ thì $a \star b \in H$
````
 
Nghĩa là toán tử $\star$ đóng với các phần tử trong $H$.

````{prf:example}
Xét nhóm $(\mathbb{Z}, +)$ như trên. Ta xét tập con gồm các số chẵn của nó

$$2\mathbb{Z} = \{ \ldots, -4, -2, 0, 2, 4, \ldots \}$$

Ta thấy rằng tổng hai số chẵn vẫn là số chẵn, nghĩa là phép cộng số nguyên đóng trên $2\mathbb{Z}$.

Do đó $(2\mathbb{Z}, +)$ là nhóm con của $(\mathbb{Z}, +)$.

Tổng quát, mọi tập hợp có dạng $n \mathbb{Z}$ đều là nhóm con của $(\mathbb{Z}, +)$.
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

```{admonition} **Chứng minh.**
:class: danger, dropdown
Nếu hai coset rời nhau thì không có gì phải nói. Ta chứng minh trường hợp còn lại.

Giả sử $g_1 H \cap g_2 H \neq \emptyset$. Như vậy tồn tại $h_1, h_2 \in H$ mà $g_1 h_1 = g_2 h_2$.

Do $h_1^{-1} \in H$, ta có $g_1 = g_2 h_2 h_1^{-1}$, nghĩa là $g_1 \in g_2 H$.

Mà mọi phần tử trong $g_1 H$ có dạng $g_1 h$ nên $g_1 h = g_2 h_2 h_1^{-1} h$. Do $H$ là nhóm con của $G$ nên $h_2 h_1^{-1} h \in H$.

Từ đó $g_1 H \subseteq g_2 H$. Tương tự ta cũng có $g_2 H \subseteq g_1 H$. Vậy $g_1 H = g_2 H$.
```

### Normal Subgroup

````{prf:definition} Normal Subgroup, nhóm con chuẩn tắc
Nhóm con $H$ của $G$ được gọi là **normal subgroup** nếu với mọi $g \in G$ ta có coset trái trùng với coset phải.

$$\begin{equation*}
    gH = Hg \quad \text{ với mọi } g \in G
\end{equation*}$$
````

Nếu $H$ là normal subgroup của $G$ ta ký hiệu $H \triangleleft G$. Khi đó, với mọi $a, b \in G$ thì $(a H) (b H) = (ab) H$.

````{prf:definition} Quotient Group, nhóm thương
Với nhóm $G$ và normal subgroup của nó là $H$.

Quotient Group được ký hiệu là $G / H$ và được định nghĩa là tập hợp các coset tương ứng với normal subgroup $H$.

$$G / H = \{gH : g \in H \}$$

Ta thấy rằng điều này chỉ xảy ra nếu $H$ là normal subgroup.
````

Quotient Group còn được gọi là Factor Group - *nhóm nhân tử*.

````{prf:example}
Với nhóm $\mathbb{Z}$ và normal subgroup của nó là $2\mathbb{Z}$.
Ta thấy $\mathbb{Z} / 2 \mathbb{Z} = \{0 + 2 \mathbb{Z}, 1 + 2 \mathbb{Z}\}$
````