# Курс высшей математики: Теория вероятностей

Lời giải cho quyển sách {cite}`Pet08`. Đây là quyển mình được học trên trường.

## Xác suất không liên tục

**Bài 1.** Có 10 đội được chia ngẫu nhiên làm hai nhóm. Tính xác xuất để hai đội mạnh nhất vào hai nhóm khác nhau? ... cùng một nhóm? ... cùng vào nhóm thứ nhất?

**Giải.** 1. Một đội mạnh có $C^1_2$ cách chọn, đội còn lại sẽ vào nhóm còn lại. Tiếp theo, chọn 4 đội cho nhóm đầu có $C^4_8$ cách, 4 đội cho nhóm còn lại có $C^4_4$ cách. Không gian mẫu là $C^5_{10} \cdot C^5_5$. Vậy đáp án là $\dfrac{5}{9}$.
2. Hai đội mạnh vào cùng một nhóm, có $C^1_2$ cách. Chọn 3 đội cho nhóm đó có $C^3_8$ cách. Nhóm còn lại sẽ có $C^5_5$ cách. Không gian mẫu là $C^5_{10} \cdot C^5_5$. Vậy đáp án là $\dfrac{4}{9}$.
3. Hai đội mạnh đều vào nhóm đầu nên chỉ có 1 cách chọn. Chọn 3 đội còn lại của nhóm đầu có $C^3_8$ cách. Chọn 5 đội cho nhóm còn lại có $C^5_5$ cách. Không gian mẫu là $C^5_{10} \cdot C^5_5$. Vậy đáp án là $\dfrac{2}{9}$.

---

**Bài 2.** Một bộ bài đầy đủ có 52 lá. Lấy ngẫu nhiên ra ba lá. Tính xác suất để ba lá đó là 3, 7 và át? Tính xác suất để ba lá đó được lấy theo thứ tự trên?

**Giải.**

1. Không gian mẫu là $C^3_{52}$. Lấy một trong bốn con 3 có $C^1_4$ cách, tương tự cho lấy con 7 có $C^1_4$ cách và lấy con át có $C^1_4$ cách. Vậy đáp án là $\dfrac{4 \cdot 4 \cdot 4}{C^3_{52}} = \dfrac{16}{5525}$.
2. Không gian mẫu là $A^3_{52}$ vì có xét thứ tự. Cách chọn ba lá bài vẫn như trước. Vậy đáp án là $\dfrac{4 \cdot 4 \cdot 4}{A^3_{52}} = \dfrac{8}{16575}$.

---

**Bài 3.** Trên đoạn thẳng $OA$ độ dài $L$ chọn ngẫu nhiên hai điểm $B$ và $C$, điều kiện là $C$ nằm bên phải so với $B$. Tính xác suất để độ dài $BC$ nhỏ hơn độ dài $OB$.

**Giải.**

```{figure} figures-pet08/ch01-ex03.jpg
```

Gọi $L$ là độ dài đoạn $OA$. Đặt $x$ là độ dài $OB$ và $y$ là độ dài $BC$. Khi đó các độ dài này phải thỏa mãn các phương trình

$$\begin{equation*}
    \begin{cases}
        y < x \\
        0 < x + y < L \\
        x > 0, y > 0
    \end{cases}
\end{equation*}$$

Xác suất trên tương ứng biểu diễn hình học. Khi đó xác suất là tỉ lệ diện tích:

1. Không gian mẫu là tam giác vuông nên diện tích là $\dfrac{L^2}{2}$.
2. Vùng giới hạn bởi các đường thẳng $y = 0$, $y = x$ và $x + y = L$ là tam giác với diện tích là $\dfrac{L \cdot \dfrac{L}{2}}{2} = \dfrac{L^2}{4}$.

Đáp án: $\dfrac{1}{2}$

---

**Bài 4.** Có 10 bilet nằm trên bàn giám thị được đánh số từ 1 tới 10. Tính xác suất để các sinh viên lấy bilet theo thứ tự từ 1 tới 10.

**Giải.** Không gian mẫu là $10!$ cách lấy 10 bilet theo tứ tự bất kì.

Để lấy 10 bilet theo thứ tự, chỉ có duy nhất một cách lấy lần lượt 1, 2, \dots.

Đáp án: $\dfrac{1}{10!}$

---

**Bài 5.** Bốn người vào thang máy ở tầng 1 của tòa nhà 9 tầng. Biết rằng xác suất mỗi người rời khỏi thang máy là như nhau cho các tầng từ 2 tới 9. Tính xác suất để: a) mọi người rời thang máy ở các tầng khác nhau; b) mọi người rời thang máy cao hơn tầng 5; c) ở tầng 3 không ai rời thang máy

**Giải.** Không gian mẫu là $8^4$ vì mỗi người đều có 8 cách chọn ra các tầng từ 2 tới 9.

a) Chọn 4 tầng mà mỗi người sẽ ra, có $A^4_8$ cách vì thứ tự có thể khác nhau. Đáp án là $\dfrac{A^4_8}{8^4} = \dfrac{105}{256}$.

b) Tầng cao hơn 5 có 4 phương án 6, 7, 8, 9. Khi đó mỗi người có 4 cách chọn nên bốn người có $4^4$ cách chọn. Đáp án là $\dfrac{4^4}{8^4} = \dfrac{1}{16}$.

c) Do không ai rời thang máy tầng 3 nên mỗi người có 7 cách chọn 2, 4, 5, 6, 7, 8 và 9. Do đó số cách chọn của bốn người là $7^4$. Đáp án là $\dfrac{7^4}{8^4} = \dfrac{2401}{4096}$.

---

**Bài 6.** Lấy ngẫu nhiên bốn chữ số và xếp chúng theo vị trí bất kì. Tính xác suất để thu được số có 4 chữ số? Tính xác suất để thu được số có 4 chữ số chia hết cho 5?

**Giải.** Không gian mẫu là $10^4$ vì có 10 chữ số từ 0 tới 9.

1. Để tạo thành số có 4 chữ số thì chữ số đầu phải khác 0 nên có 9 cách chọn. Ba vị trí còn lại mỗi vị trí 10 cách chọn. Như vậy số cách chọn là $9 \cdot 10^3$ nên đáp án là $\dfrac{9}{10}$.
2. Tương tự, để tạo thành số có 4 chữ số thì chữ số đầu có 9 cách chọn. Vị trí cuối phải là 0 hoặc 5 để chia hết cho 5. Hai chữ số ở giữa tùy ý nên có $10^2$ cách. Như vậy số cách chọn là $9 \cdot 2 \cdot 10^2$ nên đáp án là $\dfrac{9}{50}$.

---

**Bài 7.** Có 20 bilet exam trên bàn giám thị theo thứ tự ngẫu nhiên. 10 sinh viên lần lượt bốc bilet ngẫu nhiên. Tính xác suất để bilet số 1 và 2 không được chọn.

**Giải.** Không gian mẫu là $A^{10}_{20}$ do các sinh viên bốc lần lượt nên sẽ có thứ tự.

Biến cố bilet số 1 và 2 không được chọn, như vậy sẽ còn 18 trường hợp và 10 sinh viên sẽ bốc ngẫu nhiên 10 bilet trong này. Do đó có $A^{10}_{18}$ cách.

Đáp án: $\dfrac{A^{10}_{18}}{A^{10}_{20}} = \dfrac{9}{38}$.

---

**Bài 8.** Trong hộp có 6 quả bóng trắng, 4 quả bóng đen và 2 quả bóng đỏ. Lấy ngẫu nhiên 4 quả bóng. Tính xác suất để trong số 4 quả đó chỉ có bóng đen và bóng đỏ.

**Giải.** Có tất cả $6+4+2=12$ quả bóng. Không gian mẫu là $C^4_{12}$.

Bóng đen và bóng đỏ có tất cả $4+2=6$ quả. Lấy 4 trong số đó có $C^4_6$ cách.

Đáp án: $\dfrac{C^4_6}{C^4_{12}} = \dfrac{1}{33}$.

---

**Bài 9.** Có 10 quyển sách, trong đó có 3 quyển màu đỏ, được xếp theo thứ tự ngẫu nhiên trên kệ. Tính xác suất để 3 quyển màu đỏ nằm liền kề nhau.

**Giải.** Không gian mẫu là $10!$.

Nếu xem 3 quyển đỏ là cùng 1 khối thì lúc này trên kệ có 8 quyển. Số cách chọn là $8!$. Bên trong khối đó, 3 quyển màu đỏ có thể xếp theo thứ tự bất kì nên có $3!$ hoán vị. Như vậy tổng số cách xếp là $8! \cdot 3!$.

Đáp án là $\dfrac{8! \cdot 3!}{10!} = \dfrac{1}{15}$.

---

**Bài 10.** Gieo 3 con súc sắc. Tính xác suất các biết cố: $A$ -- các súc sắc cho các số khác nhau; $B$ -- các súc sắc ra cùng số.

**Giải.** Không gian mẫu là $6^3$.

1. Các súc sắc cho số khác nhau nên có $A^3_6$ cách chọn vì có tính hoán vị. Đáp án là $P(A) = \dfrac{A^3_6}{6^3} = \dfrac{5}{9}$.
2. Các súc sắc ra cùng số có 6 trường hợp. Đáp án là $P(B) = \dfrac{6}{6^3} = \dfrac{1}{36}$.

---

**Bài 11.** Trong tủ có 5 đôi tất. Lấy ngẫu nhiên 2 chiếc tất. Tính xác suất để 2 chiếc tất đó cùng đôi.

**Giải.** Không gian mẫu $C^2_{10}$.

Lấy 2 chiếc cùng đôi nghĩa là lấy 1 trong 5 đôi. Vậy có 5 cách chọn.

Đáp án: $\dfrac{5}{C^2_{10}} = \dfrac{1}{9}$.

---

**Bài 13.** Trong nhóm có 4 nam và 4 nữ được chia thành hai nhóm nhỏ, mỗi nhóm 4 người. Tính xác suất để ở mỗi nhóm nhỏ có 2 nam và 2 nữ.

**Giải.** Do có tất cả 8 người nên để chia thành hai nhóm nhỏ thì ta chọn 4 người cho nhóm đầu, có $C^4_8$ cách. Nhóm thứ hai có $C^4_4$ cách. Tuy nhiên có khả năng bị lặp (chọn A--B rồi C--D hoàn toàn giống chọn C--D rồi A--B). Do đó không gian mẫu cần chia $2!$ nên $\lvert \Omega \rvert = \dfrac{C^4_8 \cdot C^4_4}{2!} = 35$ cách.

Tương tự, ta chọn 2 nam cho nhóm đầu thì có $C^2_4$ cách và cho nhóm thứ hai có $C^2_2$ cách. Như vậy có 6 cách chia 4 nam vào 2 nhóm. Nữ cũng vậy, có 6 cách. Theo bên trên, hai nhóm này có thể bị lặp nên cần phải chia $2!$. Suy ra số cách chia mỗi nhóm 2 nam 2 nữ là $\dfrac{6 \cdot 6}{2!} = 18$.

Đáp án: $\dfrac{18}{35}$.

---

**Bài 14.**
Bên trong hình tròn bán kính $R$ chọn ngẫu nhiên một điểm. Tính xác suất để điểm đó: a) nằm bên trong hình vuông nội tiếp; b) nằm bên trong tam giác đều nội tiếp.

**Giải.** Bài này sử dụng xác suất hình học. Khi đó không gian mẫu là diện tích hình tròn bán kính $R$, hay $\lvert \Omega \rvert = \pi R^2$.

a) Biến cố điểm nằm trong hình vuông nội tiếp có xác suất bằng diện tích hình vuông chia diện tích hình tròn. Hình vuông nội tiếp đường tròn bán kính $R$ có đường chéo bằng $2R$ nên cạnh là $R \sqrt{2}$. Đáp án là $\dfrac{2R^2}{\pi R^2} = \dfrac{2}{\pi}$.

b) Tương tự, tam giác nội tiếp thì cạnh nối từ tâm tới đỉnh là $R$, bằng $2R/3$ độ dài đường cao nên suy ra đường cao là $3R/2$. Suy ra cạnh là $R \sqrt{3}$. Diện tích tam giác nội tiếp là $\dfrac{R \sqrt{3} \cdot 3R/2}{2} = \dfrac{3\sqrt{3} \cdot R^2}{4}$ nên đáp án là $\dfrac{3\sqrt{3}}{4 \pi}$.

---

**Bài 15.** Trong một ngày có hai chuyến tàu cập cảng để dỡ hàng. Chuyến tàu thứ nhất cần 6 tiếng để dỡ hàng, trong khi chuyến tàu thứ hai cần 8 tiếng. Hai chuyến tàu đến cảng không phụ thuộc vào nhau. Tính xác suất để không chuyến tàu nào phải chờ chuyến tàu kia dỡ hàng xong mới được cập cảng.

**Giải.** Gọi $x$ là thời gian chuyến tàu đầu cập cảng. Do mất 6 giờ để dỡ hàng nên tàu phải cập cảng trước 18 giờ. Suy ra $0 \leqslant x \leqslant 18$.

Tương tự, gọi $y$ là thời gian chuyến tàu thứ hai cập cảng. Suy ra $0 \leqslant y \leqslant 16$.

Đến đây ta có hai trường hợp:

1. Chuyến tàu đầu cập cảng trước. Khi đó chuyến tàu thứ hai phải đến sau khi chuyến tàu đầu dỡ hàng xong. Do đó $y \geqslant x + 6$.
2. Chuyến tàu thứ hai cập cảng trước. Tương tự, chuyến tàu đầu phải cập cảng sau khi chuyến thứ hai dỡ hàng xong. Do đó $x \geqslant y + 8$.

Không gian mẫu là diện tích hình chữ nhật giới hạn bởi $x=0$, $x=18$, $y=0$ và $y=16$.

Không gian biến cố nằm trong hình giới hạn bởi các đường thẳng $x=0$, $x=18$, $y=0$, $y=16$, $x+6=y$ và $x-8=y$.

Đáp án: $\dfrac{25}{72}$.

## Quy tắc cộng và nhân xác suất

**Bài 1.** Xác suất bóng đèn hoạt động tốt trong khoảng thời gian xác định của mỗi phần tử là 0,8. Một hệ thống có 3 phần tử như hình. Tính độ hoạt động tốt trong mỗi phần tử.

**Giải.** Nào vẽ hình rồi giải sau :)))

---

**Bài 2.** Trong hộp có 7 quả bóng trắng và 3 quả bóng đen. Lấy ngẫu nhiên lần lượt từng quả đến khi lấy được bóng đen. Tính xác suất đến khi dừng lại lấy được 4 quả bóng nếu: a) lấy có trả lại; b) lấy không trả lại.

**Giải.** Không gian mẫu gồm các cách lấy ra 4 quả bóng.

a) Khi lấy có trả lại, ở mỗi lần lấy có 10 cách chọn nên không gian mẫu $\lvert \Omega \rvert = 10^4$. Theo đề bài, nếu lấy có trả lại 4 quả bóng, 3 quả đầu là bóng trắng và có $7^3$ cách chọn. Quả bóng cuối màu đen, có 3 cách chọn. Như vậy có $7^3 \cdot 3$ cách chọn. Đáp án là $\dfrac{1029}{10000}$.

b) Khi lấy không trả lại, không gian mẫu là số cách lấy 4 quả bóng từ 10 quả bóng có thứ tự nên $\lvert \Omega \rvert = A^4_{10}$. Số cách chọn 4 quả sao cho 3 quả đầu màu trắng là $A^3_7$, và quả cuối màu đen là $A^1_3$. Đáp án là $\dfrac{A^3_7 \cdot A^1_3}{A^4_{10}} = \dfrac{1}{8}$.

---

**Bài 3.** Trong một bộ domino có 28 quân lấy ngẫu nhiên 7 quân. Tính xác suất có ít nhất một quân có nút 6.

**Giải.** Gọi $A$ là biến cố ít nhất một quân có nút 6. Khi đó $\bar{A}$ là biến cố không có quân nào có nút 6.

Không gian mẫu là $A^7_{28}$.

Do $\bar{A}$ không chứa các quân có nút 6 nên sẽ có $28-7=21$ quân (bỏ các cặp 0--6, 1--6, ..., 6--6).

Suy ra $P(\bar{A}) = \dfrac{A^7_{21}}{A^7_{28}} = \dfrac{323}{3289}$.

Đáp án: $P(A) = 1 - P(\bar{A}) = \dfrac{2966}{3289}$.

---

**Bài 4.** Tung 4 cục súc sắc. Tính xác suất để chúng ra các mặt khác nhau.

**Giải.** Đáp án: $\dfrac{A^4_6}{6^4} = \dfrac{5}{18}$.

---

**Bài 5.** Trong hộp có 5 quả bóng trắng, 7 quả bóng đỏ và 8 quả bóng xanh. Lấy ngẫu nhiên ra 2 quả. Tính xác suất để hai quả đó cùng màu.

**Giải.** Gọi $A$ -- biến cố lấy hai quả bóng cùng màu.

Gọi $A_1, A_2, A_3$ lần lượt là biến cố lấy hai quả bóng trắng, hai quả bóng đỏ và hai quả bóng xanh.

Khi đó $A = A_1 \cup A_2 \cup A_3$.

Đáp án: $P(A) = P(A_1) + P(A_2) + P(A_3) = \dfrac{C^2_5 + C^2_7 + C^2_8}{C^2_{5+7+8}} = \dfrac{59}{190}$.

---

**Bài 6.** Hai cung thủ bắn tên đồng thời độc lập nhau. Xác suất mỗi người bắn trúng là 0,2. Tính xác suất để chỉ một người bắn trúng.

**Giải.** Chọn một trong hai người bắn trúng, có 2 cách.

Nếu người đó bắn trúng thì xác suất là 0,2. Người còn lại sẽ bắn trượt với xác suất 0,8.

Đáp án: $2 \cdot 0,2 \cdot 0,8 = 0,32$.

---

**Bài 7.** 12 đội bóng tham gia giải đấu. Trong giải đấu có 4 giải thưởng sẽ được trao cho 4 đội xuất sắc nhất. Giả sử 12 đội được chia thành 4 nhóm được đánh số, mỗi nhóm 5 đội. Tính xác suất để mỗi nhóm có một đội đạt giải? Tính xác suất để nhóm đầu không có đội nào đạt giải.

**Giải.** Số cách chọn 5 đội cho nhóm đầu là $C^5_{20}$, cho nhóm thứ hai là $C^5_{15}$, cho nhóm thứ ba là $C^5_{10}$ và nhóm cuối là $C^5_5$. Do có xét thứ tự nhóm nên vẫn tính các hoán vị. Suy ra

$$\begin{equation*}
    \lvert \Omega \rvert = C^5_{20} \cdot C^5_{15} \cdot C^5_{10} \cdot C^5_5
\end{equation*}$$

Trong 4 đội đạt giải, chọn một đội cho vào nhóm 1 thì có 4 cách chọn. Tiếp theo chọn 4 đội trong 16 đội không đạt giải vào nhóm 1 thì có $C^4_{16}$ cách. Tương tự cho các nhóm 2, 3, 4 nên đáp án là

$$\begin{equation*}
    P(A) = \dfrac{4 \cdot C^4_{16} \cdot 3 \cdot C^4_{12} \cdot 2 \cdot C^4_8 \cdot 1 \cdot C^4_4}{C^5_{20} \cdot C^5_{15} \cdot C^5_{10} \cdot C^5_5} = \dfrac{125}{969}
\end{equation*}$$

Nếu nhóm đầu không có đội nào đạt giải, chọn 5 trong số 16 đội không đạt giải thì có $C^5_{16}$ cách. Lúc này còn lại 15 đội. Chọn 5 đội cho nhóm thứ 2, 5 đội cho nhóm thứ 3 và 5 đội cho nhóm thứ 4 có $C^5_{15} \cdot C^5_{10} \cdot C^5_5$ cách. Đáp án câu (b) là

$$\begin{equation*}
    P(B) = \dfrac{C^5_{16} \cdot C^5_{15} \cdot C^5_{10} \cdot C^5_{5}}{C^5_{20} \cdot C^5_{15} \cdot C^5_{10} \cdot C^5_5} = \dfrac{91}{323}
\end{equation*}$$

---

**Bài 8.** Trong hộp đầu có 2 quả bóng trắng và 3 quả bóng đen, trong hộp thứ hai có 1 trắng và 2 xanh, trong hộp thứ ba có 3 trắng và 1 đỏ. Từ mỗi hộp lấy ngẫu nhiên một quả bóng. Tính xác suất các biến số sau: $A$ -- \{ chỉ lấy ra một bóng trắng \}; $B$ -- \{ lấy ít nhất một bóng trắng \}; $C$ -- \{ lấy ra các màu khác nhau \}.

**Giải.** Không gian mẫu là $\lvert \Omega \rvert = (2 + 3) \cdot (1 + 2) \cdot (3 + 1) = 60$.

Đặt $A_1, A_2, A_3$ lần lượt là biến cố quả bóng trắng lấy từ hộp 1, 2 và 3. Khi đó $A = A_1 \cup A_2 \cup A_3$.

- Nếu quả bóng trắng lấy từ hộp 1 thì có 2 cách chọn. Ở hộp thứ hai và thứ ba phải lấy ra quả khác màu trắng nên có $2 \cdot 1$ cách chọn. Suy ra $P(A_1) = \dfrac{2 \cdot 2 \cdot 1}{60} = \dfrac{1}{15}$.
- Nếu quả bóng trắng lấy từ hộp 2 thì có 1 cách chọn. Ở hộp đầu và hộp thứ ba phải lấy ra quả khác màu trắng nên có $3 \cdot 1$ cách. Vậy $P(A_2) = \dfrac{1 \cdot 3 \cdot 1}{60} = \dfrac{1}{20}$.
- Nếu quả bóng trắng lấy từ hộp 3 thì có 3 cách chọn. Ở hộp đầu và hộp thứ hai lấy ra quả khác màu trắng có $3 \cdot 2$ cách chọn. Vậy $P(A_3) = \dfrac{3 \cdot 3 \cdot 2}{60} = \dfrac{3}{10}$.

Như vậy $P(A) = P(A_1) + P(A_2) + P(A_3) = \dfrac{1}{15} + \dfrac{1}{20} + \dfrac{3}{10} = \dfrac{5}{12}$.

Do $B$ là biến cố lấy ít nhất một bóng trắng nên $\bar{B}$ là biến cố không lấy ra bóng trắng nào. Khi đó ở hộp 1 có 3 cách chọn (đen), hộp 2 có 2 cách chọn (xanh) và hộp 3 có 1 cách chọn (đỏ). Suy ra $P(\bar{B}) = \dfrac{3 \cdot 2 \cdot 1}{60} = \dfrac{1}{10}$.

Như vậy $P(B) = 1 - P(\bar{B}) = \dfrac{9}{10}$.

Khi lấy ra ba quả bóng khác màu nhau có các trường hợp theo thứ tự hộp là:

- trắng--xanh--đỏ: có $2 \cdot 2 \cdot 1$ cách chọn
- đen--trắng--đỏ: có $3 \cdot 1 \cdot 1$ cách chọn
- đen--xanh--trắng: có $3 \cdot 2 \cdot 3$ cách chọn
- đen--xanh--đỏ: có $3 \cdot 2 \cdot 1$ cách chọn

Như vậy $P(C) = \dfrac{2 \cdot 2 \cdot 1 + 3 \cdot 1 \cdot 1 + 3 \cdot 2 \cdot 3 + 3 \cdot 2 \cdot 1}{60} = \dfrac{31}{60}$.

---

**Bài 9.** Một bộ bài gồm 36 lá. Lấy ngẫu nhiên hai lá. Tính xác suất để hai lá đó có màu đỏ.

**Giải.** Không gian mẫu $\lvert \Omega \rvert = C^2_{26}$.

Lấy hai trong $36/2=18$ lá đỏ có $C^2_{18}$ cách.

Đáp án: $\dfrac{C^2_{18}}{C^2_{26}} = \dfrac{17}{70}$.

---

**Bài 10.** Trong thùng có 3 bóng đèn hỏng và 7 bóng đèn tốt. Lấy ngẫu nhiên các bóng lần lượt đến khi lấy được 2 bóng tốt thì dừng. Tính xác suất để lấy một nửa số bóng đèn.

**Giải.** Không gian mẫu là $A^5_{10}$.

Trong số bốn bóng đèn đầu sẽ có một bóng tốt và 3 bóng hỏng. Bóng đèn thứ 5 sẽ là bóng tốt. Như vậy ta chọn vị trí cho bóng tốt trong 4 vị trí đầu, có 4 cách chọn. Chọn bóng tốt cho vị trí đó có 7 cách chọn. Chọn 3 bóng hỏng cho 3 vị trí còn lại có thứ tự, có $A^3_3$ cách.

Chọn bóng đèn tốt cho vị trí thứ 5 có 6 cách chọn.

Đáp án: $\dfrac{4 \cdot 7 \cdot A^3_3 \cdot 6}{A^5_{10}} = \dfrac{1}{30}$.

## Quy tắc cộng và nhân xác suất (tiếp theo)

**Bài 1.** Từ một bộ bài lấy ngẫu nhiên lần lượt bốn lá. Tính xác suất để tất cả các lá khác chất nhau? Tính xác suất để tất cả các lá khác số nhau?

**Giải.** Bộ bài có 36 lá (bài Nga) nên có không gian mẫu $\lvert \Omega \rvert = A^4_{36}$.

Gọi $A$ là biến cố tất cả các lá khác chất nhau.

- Chọn chất cho lá thứ nhất có 4 cách chọn. Chọn lá thứ nhất có 9 cách chọn (trong chất đó).
- Chọn chất cho lá thứ hai có 4 cách chọn. Chọn lá thứ hai có 9 cách chọn (trong chất đó).
- Tương tự cho lá thứ ba và thứ tư.

Như vậy $\lvert \Omega_A \rvert = 4! \cdot 9^4$. Đáp án là $P(A) = \dfrac{\lvert \Omega_A \rvert}{\lvert \Omega \rvert} = \dfrac{729}{6545}$.

Gọi $B$ là biến cố tất cả các lá có số khác nhau.

- Chọn số cho lá thứ nhất có 9 cách chọn. Chọn chất cho lá đó có 4 cách chọn.
- Chọn số cho lá thứ hai có 8 cách chọn. Chọn chất cho lá đó có 4 cách chọn.
- Tương tự cho lá thứ ba và thứ  tư.

Như vậy $\lvert \Omega_B \rvert = A^4_9 \cdot 4^4$. Đáp án là $P(B) = \dfrac{\lvert \Omega_B \rvert}{\lvert \Omega \rvert} = \dfrac{512}{935}$.

---

**Bài 2.** Trong rổ có 10 quả bóng tennis, 7 quả mới và 3 quả đã qua sử dụng. Lấy ngẫu nhiên 2 quả từ rổ cho trận đấu rồi trả lại. Tới trận đấu thứ hai cũng lấy ngẫu nhiên 2 quả. Tính xác suất để ở trận thứ hai lấy được 2 quả mới.

**Giải.** Sau khi chơi xong trận đầu thì những quả bóng mới sẽ trở thành bóng đã qua sử dụng.

Đặt $B$ là biến cố trận thứ hai lấy được 2 quả mới.

Đặt $A_1$, $A_2$ và $A_3$ lần lượt là biến cố trận đầu lấy được 2 quả bóng mới, 1 mới 1 đã qua sử dụng và 2 quả đã qua sử dụng. Ba biến cố này hợp thành biến cố đầy đủ cho việc lấy 2 quả ở trận đầu.

Theo công thức xác suất toàn phần:

$$\begin{equation*}
    P(B) = P(A_1) P(B \vert A_1) + P(A_2) P(B \vert A_2) + P(A_3) P(B \vert A_3)
\end{equation*}$$

Nếu ở trận đầu lấy 2 quả mới, ta có $P(A_1) = \dfrac{C^2_7}{C^2_{10}} = \dfrac{7}{15}$. Sau khi trận đầu kết thúc, số bóng mới là $7-2=5$ và số bóng đã qua sử dụng là $3+2=5$ nên $P(B \vert A_1) = \dfrac{C^2_5}{C^2_{10}} = \dfrac{2}{9}$.

Nếu ở trận đầu lấy 1 quả mới và 1 quả đã qua sử dụng, ta có $P(A_2) = \dfrac{C^1_7 \cdot C^1_3}{C^2_{10}} = \dfrac{7}{15}$. Sau khi trận đầu kết thúc, số bóng mới là 6 và số bóng đã qua sử dụng là 4 nên $P(B \vert A_2) = \dfrac{C^2_6}{C^2_{10}} = \dfrac{1}{3}$.

Nếu ở trận đầu lấy 2 quả đã qua sử dụng thì $P(A_3) = \dfrac{C^2_3}{C^2_{10}} = \dfrac{1}{15}$. Sau khi trận đầu kết thúc, số bóng mới vẫn là 7 và số bóng đã qua sử dụng vẫn là 3 nên $P(B \vert A_3) = \dfrac{C^2_7}{C^2_{10}} = \dfrac{7}{15}$.

Đáp án: $P(B) = \dfrac{7}{15} \cdot \dfrac{2}{9} + \dfrac{7}{15} \cdot \dfrac{1}{3} + \dfrac{1}{15} \cdot \dfrac{7}{15} = \dfrac{196}{675} \approx 0,29$.

---

**Bài 3.** Trên mỗi cánh máy bay có 2 động cơ. Xác suất bị lỗi của mỗi động cơ trong một chuyến bay là $p$. Chuyến bay sẽ thành công nếu ở mỗi cách có ít nhất một động cơ hoạt động bình thường. Tính xác suất chuyến bay thành công.

**Giải.** Gọi $A$ là biến cố ở một cánh có ít nhất một động cơ hoạt động. Suy ra $\bar{A}$ là biến cố không động cơ nào hoạt động ở cả một cánh.

Như vậy $P(\bar{A}) = p^2$ nên $P(A) = 1-p^2$. Áp dụng cho hai bên cánh (theo quy tắc nhân) ta có đáp án là $(1-p^2)^2$.

---

**Bài 4.** Sinh viên biết 20 trong 30 câu hỏi. Để qua bài thi cần trả lời đúng 2 câu hỏi bắt buộc hoặc trả lời đúng 1 trong 2 câu bắt buộc cộng thêm 1 câu hỏi phụ. Tính xác suất để sinh viên vượt qua bài thi?

**Giải.** Ở đây cần hiểu là sinh viên biết 20 câu trong số 30 câu, 10 câu kia là câu hỏi phụ. Khi đó có hai trường hợp:

Trường hợp 1 là sinh viên trả lời đúng 2 câu trong số 20 câu sinh viên biết nên xác suất là $\dfrac{A^2_{20}}{A^2_{30}}$.

Trường hợp 2 là sinh viên trả lời đúng 1 trong 2 câu bắt buộc (có $A^2_{20} \cdot 2$ cách chọn) và 1 câu hỏi phụ (10 cách chọn) nên xác suất là $\dfrac{A^2_{20} \cdot 2 \cdot 10}{A^3_{30}}$. Tổng số câu sinh viên trả lời là 3.

Đáp án: $\dfrac{A^2_{20}}{A^2_{30}} + \dfrac{A^2_{20} \cdot 2 \cdot 10}{A^3_{30}} = \dfrac{152}{203}$.
