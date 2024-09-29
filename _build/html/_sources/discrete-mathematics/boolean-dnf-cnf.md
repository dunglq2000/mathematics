## Dạng DNF và CNF

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
