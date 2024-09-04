## Group homomorphism

```{contents}
```

### Đồng cấu nhóm

````{prf:definition} Homomorphism, Đồng cấu nhóm
Xét hai nhóm $(G, \star)$ và $(H, *)$ và một ánh xạ $f: G \to H$.
Ánh xạ $f$ được gọi là **đồng cấu** (hay **homomorphism**) nếu với mọi $g_1$, $g_2$ thuộc $G$ ta có $f(g_1 \star g_2) = f(g_1) * f(g_2)$.
````

Do $g_1$, $g_2$ là các phần tử thuộc $G$ nên toán tử giữa chúng là $\star$. Trong khi đó $f(g_1)$, $f(g_2)$ là các phần tử thuộc $H$ nên toán tử giữa chúng là $*$.

````{prf:remark}
1. Gọi $e_G$ là phần tử đơn vị của $G$ và $e_H$ là phần tử đơn
    vị của $H$. Khi đó $f(e_G) = e_H$
2. Với mọi phần tử $g \in G$, nếu $g^{-1}$ là nghịch đảo của nó trong $G$ thì $f(g^{-1}) = f(g)^{-1}$
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
1. Nếu $e_G$ là phần tử đơn vị của $G$ thì với mọi $g \in G$ ta có $g \star e_G = e_G \star g = g$. Ta lấy $f$ cả ba vế và theo định nghĩa homomorphism thu được $f(g \star e_G) = f(e_G \star g) = f(g)$, suy ra $f(g) * f(e_G) = f(e_G) * f(g) = f(g)$. Đẳng thức trên đúng với mọi $g \in G$ nên đúng với mọi $f(g)$, suy ra $f(e_G)$ là phần tử đơn vị trong nhóm $(H, *)$ và do đó $f(e_G) = e_H$
2. Từ việc tìm ra phần tử đơn vị, ta cũng chứng minh được tính chất nghịch đảo trên.
```

### Các loại homomorphism

Tương tự như ánh xạ, chúng ta có các loại homomorphism sau

````{prf:definition} Monomorphism, Đơn cấu
Ánh xạ được gọi là **đơn cấu** (hay **monomorphism**) nếu nó là ánh xạ one-to-one (đơn ánh). Nói cách khác, với mọi $g_1 \neq g_2$ và $g_1$, $g_2 \in G$, thì $f(g_1) \neq f(g_2)$
````

````{prf:definition} Epimorphism, Toàn cấu
Ánh xạ được gọi là **toàn cấu** (hay **epimorphism**) nếu nó là ánh xạ onto (toàn ánh). Nói cách khác, với mọi $h \in H$ thì tồn tại $g \in G$ mà $f(g) = h$.
````

````{prf:definition} Isomorphism, Đẳng cấu
Ánh xạ được gọi là **đẳng cấu** (hay **isomorphism**) nếu nó là ánh xạ one-to-one và onto (song ánh). Nói cách khác, ánh xạ này vừa là đơn cấu, vừa là toàn cấu.
````

````{prf:definition} Automorphism, Tự đẳng cấu
Ánh xạ được gọi là **tự đẳng cấu** (hay **automorphism**) nếu nó là song ánh từ nó lên chính nó. Ta ký hiệu tự đồng cấu nhóm $G$ là $\mathrm{Aut}(G)$.
````

### Hạt nhân và ảnh

Xét một homomorphism $f$ từ nhóm $(G, \star)$ tới nhóm $(H, *)$. Ta nói:

````{prf:definition} Kernel, Hạt nhân
**Hạt nhân** (hay **kernel**) của $f$ là tập hợp các phần tử của $G$ cho ảnh là $e_H$, ký hiệu là $\ker f$. Nói cách khác

$$\begin{equation}
    \ker f = \{ g \in G, f(g) = e_H \}
\end{equation}$$

Như vậy $\ker f$ là tập con của $G$.
````

````{prf:remark}
$K = \ker f$ là normal subgroup của $G$.
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
Để chứng minh, ta thấy rằng theo định nghĩa homomorphism, với $g_1, g_2 \in K$ thì $f(g_1) = f(g_2) = e_H$.

Ta có $f(g_1 \star g_2) = f(g_1) * f(g_2) = e_H * e_H = e_H$. Như vậy $g_1 \star g_2 \in K$ nên $K$ là nhóm con của $G$.

Tiếp theo để chứng minh $K$ là normal subgroup, ta chứng minh
$g K g^{-1} = K$ với mọi $g \in G$.

Do $g K g^{-1} = \{ g \star k \star g^{-1} : k \in K \}$, lấy $f$ mỗi phần tử bên trong ta có

$$f(g \star k \star g^{-1}) = f(g) * f(k) * f(g^{-1}) = 
f(g) * e_H * f(g^{-1}) = f(g) * f(g^{-1})$$

mà theo tính chất của homomorphism thì $f(g^{-1}) = f(g)^{-1}$ nên $f(g \star k \star g^{-1}) = f(g) * f(g)^{-1} = e_H$ nên $g \star k \star g^{-1} \in K$ với mọi $g \in G$, với mọi $k \in K$. Do đó $g K g^{-1} = K$ và ta có điều phải chứng minh.
```

````{prf:definition} Image, Ảnh
**Ảnh** (hay **image**) của $f$ là tập hợp tất cả giá trị nhận được khi biến các phần tử thuộc $G$ thành phần tử thuộc $H$. Nói cách khác

$$\begin{equation}
    \mathrm{im} f = \{ f(g), g \in G \}
\end{equation}$$

Như vậy $\mathrm{im} f$ là tập con của $H$.
````

Dựa trên hai khái niệm này, chúng ta có một định lý quan trọng trong lý
thuyết nhóm là **Định lý thứ nhất về sự đẳng cấu** (First isomorphism theorem).

````{prf:theorem} First isomorphism theorem
Với hai nhóm $(G, \star)$ và $(H, *)$. Xét homomorphism $f: G \to H$. Khi đó $\mathrm{im} f$ đẳng cấu (isomorphism) với nhóm thương $G / \ker f$.
````

```{admonition} **Chứng minh.**
:class: danger, dropdown
Gọi $G$, $H$ là hai nhóm và homomorphism $f: G \to H$.
Đặt $K = \ker f$. Ta xét biến đổi

$$\theta:\,\mathrm{im} f \to G / K, f(g) \to g K$$

với $g \in G$.

Ta cần chứng minh biến đổi này là ánh xạ xác định (well-defined, nghĩa là tuân theo quy tắc ánh ánh xạ, mỗi phần tử tập nguồn biến thành **một và chỉ một** phần tử tập đích), là homomorphism, là đơn ánh và là toàn ánh.

Đầu tiên ta chứng minh ánh xạ xác định. Giả sử ta có $g_1 K = g_2 K$, do $g_1$ và $g_2$ thuộc cùng coset nên $g_1^{-1} g_2 \in K$, hay $f(g_1^{-1} g_2) = e_H$.

Với $f$ là homomorphism, ta có 

$$f(g_1^{-1} g_2) = f(g_1^{-1}) f(g_2) = f(g_1)^{-1} f(g_2) = e_H$$

Suy ra $f(g_1) = f(g_2)$. Như vậy nếu $f(g_1) = f(g_2)$ thì $\theta (f(g_1)) = \theta (f(g_2))$.

Tiếp theo ta chứng minh $\theta$ là homomorphism. Do $K$ là normal subgroup của $G$ nên với mọi $g_1$, $g_2$ thuộc $G$ thì $g_1 g_2 K = (g_1 K) (g_2 K)$.

Do $f(g_1 g_2) = f(g_1) f(g_2)$ nên 

$$\theta (f(g_1 g_2)) = g_1 g_2 K = (g_1 K) (g_2 K) = \theta (f(g_1)) \theta (f(g_2))$$

Suy ra $\theta$ là homomorphism.

Dễ thấy với mọi $g \in G$ ta đều tìm được $f(g)$ và $g K$ tương ứng. Do đó $\theta$ là toàn ánh.

Để chứng minh $\theta$ là đơn ánh, giả sử $g_1 K = g_2 K$ ta có $g_1^{-1} g_2 \in K$ nên $f(g_1^{-1} g_2) = e_H$. Suy ra $f(g_1^{-1}) f(g_2) = e_H \Rightarrow f(g_1)^{-1} f(g_2) = e_H \Rightarrow f(g_1) = f(g_2)$. Như vậy $\theta$ là đơn ánh.

Kết luận, $\theta$ là song ánh. Định lý thứ nhất về sự đẳng cấu được chứng minh.
```

