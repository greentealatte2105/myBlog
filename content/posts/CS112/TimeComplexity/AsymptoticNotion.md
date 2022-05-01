---
title: "Khái niệm Tiệm Cận và Độ Phức Tạp của Thuật Toán"
date: 2022-04-18T17:15:08+07:00
author: Lê Trần Hữu Phước
draft: false
math: true
tags: ["CS112"]
categories: ["Complexity"]
---
<h1 style="text-align: center;">Khái niệm Tiệm Cận và Độ Phức Tạp của Thuật Toán</h1>

## Tóm tắt nội dung:

Bài báo cáo này nhằm giới thiệu cho bạn đọc một cái nhìn tổng quan nhất
về mặt lí thuyết dành cho các khái niệm liên quan đến vấn đề tiệm cận và cách tìm độ phức tạp của thuật toán. Bài báo cáo sẽ giới thiệu từ ý tưởng sơ khai đến những phân tích về mặt toán học của bài toán, về cách hoạt động và một số ví dụ điển hình của vấn đề trên.

Từ khóa liên quan: Độ phức tạp, Big(O), tiệm cận,complexity, Asymptotic
Notation, Ω(.) ,...

# Giới thiệu:

Phân tích (thời gian) thuật toán về cơ bản là đếm số thao tác cơ bản mà thuật toán đó thực hiện. Tuy nhiên, việc đếm chính xác số thao tác cơ bản nhiều lúc không tầm thường hoặc phụ thuộc vào dữ liệu đầu vào (ví dụ lệnh **if - then - else**). Do đó, trong thực tế phân tích thuật toán, ta chỉ đếm tương đối số thao tác cơ bản mà thôi. **Big(O)** chính là công cụ cho phép chúng ta biểu diễn tương đối độ phức tạp của thuật toán một cách đơn giản. Bài này chúng ta sẽ tìm hiểu về định nghĩa hình thức của các khái niệm như $O(.)$, $\Theta(.)$, $\Omega(.)$.

# Mục Lục:
1. [Khái Niệm Tường Minh:](#khái-niệm-tường-minh)
    1. [O-Notation là gì?](#o---notation-là-gì)
    2. [$\Omega$ - Notation là gì?](#omega---notation-là-gì)
    3. [$\Theta$ - Notation là gì?](#theta---notation-là-gì)
2. [Định nghĩa toán học:](#định-nghĩa-toán-học)
    1. [O-Notation.](#o-notation)
    2. [$\Omega$ - Notation.](#omega-notation)
    3. [$\Theta$ - Notation.](#theta-notation)


# Khái Niệm Tường Minh:
## O - Notation là gì?
> Một cách tường minh, $O(g(n))$ là tập tất cả các hàm có số bậc bé hơn hoặc bằng so với hàm $g(n)$ (với $n$ tiến đền vô cùng).

VD: 
- $n \in O(n^2)$
- $n + 20n + 2 \in O(n^2)$
- $n(n-1) \in O(n^2)$

> Giải thích: Ta thấy rằng ở hai hàm đầu tiên đều là hàm tuyến tính và vì thế chúng có số bậc thấp hơn so với $g(n) = n^2$, trong khi đó ở hàm cuối cùng thì là hàm bình phương nên có số bậc bằng với $n^2$. Tương tự, mặc khác ta có:

VD:
- $n^3 \notin O(n^2)$
- $0.00001n^3 \notin O(n^2)$

## $\Omega$ - Notation là gì?
> Ký hiệu tiếp theo, $\Omega (g(n))$ là tập các hàm có số bậc cao hơn hoặc bằng so với $g(n)$ (với $n$ tiến đến vô cùng).

VD:
- $n^3 \in \Omega(n^2)$
- $n(n-1) \in \Omega(n^2)$
- $100n + 5 \notin \Omega(n^2)$

> Giải thích: Tương tự như các ví dụ trong [O-Notation](#o---notation-là-gì), ta thấy rằng ở hai hàm đầu tiên các bậc của chúng đều lớn hơn hoặc bằng so với $g(n)$, tuy nhiên ở hàm cuối cùng thì là hàm tuyến tính nên có số bậc nhỏ hơn $g(n) = n^2$.

## $\Theta$ - Notation là gì?
> Cuối cùng, $\Theta(g(n))$ là tập các hàm có cùng số bậc với $g(n)$ (với n tiến đến vô cùng). Vì thế, tất cả các hàm số bình phương, $an^2 + bn +c$ với $a > 0$ đều thuộc $\Theta(n^2)$.

Đó là toàn bộ giới thiệu một cách tường minh về cả ba ký hiệu tiệm cận. Ở phần tiếp theo, ta sẽ đến với các định nghĩa toán học.

# Định nghĩa toán học:
## O-Notation:
> Một hàm số $t(n)$ được gọi là thuộc $O(g(n))$, ký hiệu: $t(n) \in O(g(n))$, nếu $t(n)$ được giới hạn trên bởi một số bội không đổi của $g(n)$. Nếu tồn tại một hằng số $c$ dương bà một số nguyên không âm $n_0$.

\\[t(n) \leq cg(n), \forall n \ge n_0. \\]

Để trực quan hơn, ta sẽ minh họa như Hình 1, ở đây $n$ sẽ được mở rộng là một số thực.

![Hình 1](/images/CS112/AsymptoticNotation/O-notation.jpg "Hình 1")
Hình 1: $O - Notation: t(n) \in O(g(n))$.

#### VD: Chứng minh $100n + 5 \in O(n^2)$.

> Ta có:    
    \\[ 100n + 5 \le 100n + 5n \\]
Dễ dàng xác định được $c = 105$ và $n_0 = 1$.
Lưu ý: theo định nghĩa, ta sẽ có nhiều cách chọn $c$ và $n_0$. Ta cũng có thể lập luận như sau:
    \\[ 100n + 5 \leq 100n + n \space (\forall n \ge 5) = 101n \le 101n^2 \\]
Dễ dàng ta có được $c = 101$ và $n_0 = 5$.

## $\Omega$-Notation:
> Một hàm số $t(n)$ được gọi là thuộc $\Omega(g(n))$, ký hiệu: $t(n) \in \Omega(g(n))$, nếu $t(n)$ được giới hạn dưới bởi một số bội không đổi của $g(n)$. Nếu tồn tại một hằng số $c$ dương bà một số nguyên không âm $n_0$.

\\[t(n) \ge cg(n), \forall n \ge n_0. \\]

Để trực quan hơn, ta sẽ minh họa như Hình 2, ở đây $n$ cũng sẽ được mở rộng thành một số thực.

![Hình 2](/images/CS112/AsymptoticNotation/Omega-notation.jpg "Hình 2")
Hình 2: $\Omega - Notation: t(n) \in \Omega(g(n))$.

#### VD: Chứng minh: $n^3 \in \Omega(n^2).$
> \\[n^3 \ge n^2 \space \forall n \ge 0 \\]
Ta có thể chọn $c = 1$ và $n_0 = 0$.

## $\Theta$-Notation:
> Một hàm số $t(n)$ được gọi là thuộc $\Theta(g(n))$, ký hiệu: $t(n) \in \Theta(g(n))$, nếu $t(n)$ được giới hạn trên và dưới bởi một bội số không đổi của $g(n)$. Nếu tồn tại hai hằng số $c_1$ dương và $c_2$ dương và một bội số không âm $n_0$.
\\[ c_2g(n) \le t(n) \le c_1g(n) \space \forall n \ge n_0. \\]

Để trực quan hơn, ta sẽ minh họa ở Hình 3.

![Hình 3](/images/CS112/AsymptoticNotation/Theta-notation.jpg "Hình 3")
Hình 3: $\Theta - Notation: t(n) \in \Theta(g(n))$.

#### VD: Chứng minh $n(n-1) \in \Theta(n^2)$:
> Đầu tiên, ta chứng minh bất đẳng thức bên phải:
    \\[ n(n-1) = n^2 - n \ge n^2 - \frac{1}{2}n^2 = \frac{1}{2}n^2 \space \space \forall n \ge 2. \\]
    Vậy ta xác định được $c_2 = \frac{1}{2}$, $c_1 = 1$ và $n_0 = 2.$

# Lời Kết:

$\space \space \space$ Trong thực tế, một số yếu tố khác bên cạnh phân tích tiệm cận cũng khá quan trọng trong việc chọn thuật toán sao cho tối ưu nhất đối với mỗi trường hợp, đôi khi, ta sẽ chọn thuật toán có độ phức tạp lớn hơn so với cái còn lại.

Làm rõ vấn đề này, ta sẽ xét giải thuật A có độ phức tạp lớn hơn giải thuật B. Và đây sẽ là một số lý do phổ biến:

1. Giải thuật có độ phức tạp ít hơn thường sẽ cài đặt phức tạp hơn nên sẽ mấy nhiều thời gian lập trình.
2. Hạn chế của phương pháp phân tích tiệm cận là nó sẽ chỉ xét đến trường hợp input có kích thước lớn, vì vậy đối với những trường hợp có input nhỏ, đôi khi giải thuật B sẽ làm tốt hơn so với giải thuật A.
3. Nếu giải thuật A có worst case tốt hơn B, tuy nhiên average case của B lại tốt hơn giải thuật A thì ta sẽ ưu tiên chọn giải thuật B.

# Tài Liệu Tham Khảo:
- https://www.cs.cornell.edu/courses/cs312/2004fa/lectures/lecture16.html
- Introduction to the Design and Analysis of Algorithms 3rd Edition by Anany Levitin.