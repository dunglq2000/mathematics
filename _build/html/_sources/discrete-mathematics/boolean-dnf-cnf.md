## Disjunctive và Conjunctive Normal Form

Khi xử lý các mạch logic có ba toán tử chúng ta đặc biệt quan tâm là AND, OR, NOT. Điều này khác với đại số boolean ở phần trước chỉ quan tâm phép XOR và AND - phép cộng và nhân trong $\mathrm{GF}(2)$.

Ở phần này kí hiệu:

- NOT của biến $a$ là $\neg a$.
- AND của hai biến $a$ và $b$ là $a \land b$. Chúng ta cũng có thể kí hiệu là $a \cdot b$ hoặc $ab$ như đại số boolean ở phần trước.
- OR của hai biến $a$ và $b$ là $a \lor b$. Chúng ta **KHÔNG** dùng kí hiệu $a + b$ ở đây vì phép cộng đã được dùng ở phần ANF.

Phép AND và OR có tính giao hoán, kết hợp.

### Một số luật logic

Sau đây là một số "hằng đẳng thức đáng nhớ trong logic:

1. Luật bù:
    - $a \lor \neg a = 1$,
    - $a \land \neg a = 0$.
2. Luật hấp thụ:
    - $x \lor (x \land y) = x$,
    - $x \land (x \lor y) = x$.
3. Luật đồng nhất:
    - $x \lor 0 = x$,
    - $x \land 1 = x$.
4. Luật giao hoán:
    - $x \lor y = y \lor x$,
    - $x \land y = y \land x$.
5. Luật kết hợp:
    - $x \lor (y \lor z) = (x \lor y) \lor z$,
    - $x \land (y \land z) = (x \land y) \land z$.
6. Luật phân phối:
    - $x \lor (y \land z) = (x \lor y) \land (x \lor z)$,
    - $x \land (y \lor z) = (x \land y) \lor (x \land z)$.
7. Luật De Morgan:
    - $\neg (x \land y) = \neg x \lor \neg y$,
    - $\neg (x \lor y) = \neg x \land \neg y$.

### Tổng của tích

Nếu biểu thức boolean được biểu diễn ở dạng tổng của các tích thì ta gọi là **disjunctive normal form** (hay **DNF**).

````{prf:example}
$(a \land \neg b \land \neg c) \lor (a \land b) \lor (b \land \neg c)$
````

Ở đây, mỗi tích sẽ bao gồm các **literal** (hay **đơn tử**). Ví dụ với tích $(a \land \neg b \land \neg c)$ thì các literal sẽ là $a$, $\neg b$ và $\neg c$.

Mỗi tích sẽ được gọi là **term** (hay **hạng tử**). Trong ví dụ trên có ba term là $(a \land \neg b \land \neg c)$, $(a \land b)$ và $(b \land \neg c)$.

Biểu thức boolean với $n$ biến $x_1, \ldots, x_n$ ở dạng **full disjunctive normal form** (hay **full DNF**) mỗi term của nó có đủ $n$ literal.

Ở ví dụ trên thì các term $a \land b$ và $b \land \neg c$ chỉ có hai literal nên không phải là full DNF.

````{prf:example}
Ví dụ về full DNF:

$$(a \land b) \lor (a \land \neg b) \lor (\neg a \land b)$$
````

Để chuyển một hàm boolean về dạng full DNF chúng ta có thể dùng bảng chân trị.

Đặt $f(x_1, \ldots, x_n)$ là hàm boolean cần đưa về dạng full DNF.

1. Nếu $f = 0$ thì ta không xét.
2. Nếu $f = 1$, với $i = 1, \ldots, n$ ta xây dựng term như sau:
    - nếu $x_i = 0$ thì literal là $\neg x_i$,
    - nếu $x_i = 1$ thì literal là $x_i$.

````{prf:example}
Sử dụng ví dụ ở trên

$$f(a, b, c) = (a \land \neg b \land \neg c) \lor (a \land b) \lor (b \land \neg c)$$

Bảng chân trị của $f$ sẽ có dạng

| $a$ | $b$ | $c$ | $f$ |
| --- | --- | --- | --- |
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

Ở đây $f$ nhận giá trị $1$ khi $(a, b, c)$ là các bộ $(0, 1, 0)$, $(1, 0, 0)$, $(1, 1, 0)$ và $(1, 1, 1)$.

- đối với $(0, 1, 0)$ thì term tương ứng là $\neg a \land b \land \neg c$
- đối với $(1, 0, 0)$ thì term tương ứng là $a \land \neg b \land \neg c$
- đối với $(1, 1, 0)$ thì term tương ứng là $a \land b \land \neg c$
- đối với $(1, 1, 1)$ thì term tương ứng là $a \land b \land c$

Như vậy hàm $f$ có thể viết lại là

$$f(a, b, c) = (\neg a \land b \land \neg c) \lor (a \land \neg b \land \neg c) \lor (a \land b \land \neg c) \lor (a \land b \land c)$$
````

### Tích của các tổng

Nếu biểu thức boolean được biểu diễn ở dạng tích của các tổng thì ta gọi là **conjunctive normal form** (hay **CNF**).

````{prf:example}
$(a \lor \neg b \lor \neg c) \land (a \lor b) \land (b \lor \neg c)$
````

Tương tự, mỗi tổng sẽ bao gồm các **literal** (hay **đơn tử**). Ví dụ với tổng $(a \lor \neg b \lor \neg c)$ thì các literal sẽ là $a$, $\neg b$ và $\neg c$.

Mỗi tích sẽ được gọi là **term** (hay **hạng tử**). Trong ví dụ trên có ba term là $(a \lor \neg b \lor \neg c)$, $(a \lor b)$ và $(b \lor \neg c)$.

Biểu thức boolean với $n$ biến $x_1, \ldots, x_n$ ở dạng **full conjunctive normal form** (hay **full CNF**) mỗi term của nó có đủ $n$ literal.

Ở ví dụ trên thì các term $a \lor b$ và $b \lor \neg c$ chỉ có hai literal nên không phải là full DNF.

Tương tự, để chuyển một hàm boolean về dạng full CNF chúng ta có thể dùng bảng chân trị nhưng làm ngược lại so với DNF.

Đặt $f(x_1, \ldots, x_n)$ là hàm boolean cần đưa về dạng full CNF.

1. Nếu $f = 1$ thì ta không xét.
2. Nếu $f = 0$, với $i = 1, \ldots, n$ ta xây dựng term như sau:
    - nếu $x_i = 0$ thì literal là $x_i$,
    - nếu $x_i = 1$ thì literal là $\neg x_i$.

````{prf:example}
Sử dụng ví dụ ở trên

$$f(a, b, c) = (a \lor \neg b \lor \neg c) \land (a \lor b) \land (b \lor \neg c)$$

Bảng chân trị của $f$ sẽ có dạng

| $a$ | $b$ | $c$ | $f$ |
| --- | --- | --- | --- |
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |

Ở đây $f$ nhận giá trị $0$ khi $(a, b, c)$ là các bộ $(0, 0, 0)$, $(0, 0, 1)$, $(0, 1, 1)$, và $(1, 0, 1)$.

- đối với $(0, 0, 0)$ thì term tương ứng là $a \lor b \lor c$
- đối với $(0, 0, 1)$ thì term tương ứng là $a \lor b \lor \neg c$
- đối với $(0, 1, 1)$ thì term tương ứng là $a \lor \neg b \lor \neg c$
- đối với $(1, 0, 1)$ thì term tương ứng là $\neg a \lor b \lor \neg c$

Như vậy hàm $f$ có thể viết lại là

$$f(a, b, c) = (a \lor b \lor c) \land (a \lor b \lor \neg c) \land (a \lor \neg b \lor \neg c) \land (\neg a \lor b \lor \neg c)$$
````

Chúng ta có thể sử dụng đoạn code sau của SageMath để tìm full CNF (các bạn có thể xem ở [đây](https://doc.sagemath.org/html/en/reference/logic/sage/logic/boolformula.html)):

```python
import sage.logic.propcalc as propcalc
s = propcalc.formula("(a | ~b | ~c) & (a | b) & (b | ~c)")
s.convert_cnf()
print(s)
```
