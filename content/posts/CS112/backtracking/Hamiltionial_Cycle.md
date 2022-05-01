---
title: "Hamiltonian Circuit Problem"
author: Đào Trần Anh Tuấn
date: 2022-04-13T23:14:03+07:00
draft: false
tags: ["CS112"]
categories: ["Algorithms"]
math: true
---
## Đặt vấn đề:

Chu trình Hamilton là một dạng bài toán phổ biến trong bài toán đồ thị. Vậy chu trình Hamilton là gì? Bắt đầu với định nghĩa sau:
- Cho đồ thị $G = $ { $V$, $E$ }$ $ có $V$ là tập đỉnh, $E$ là tập cạnh, gồm $n$ đỉnh:
    - Đường đi $x_0, x_1, ..., x_{n-1}, x_{n}$ gọi là đường đi Hamilton nếu: $V$ = {$x_0, x_1,...,x_{n-1}, x_n$} với $x_i \not = x_j; 0 \leq i < j \leq n.$
    - Chu trình $x_0, x_1,..., x_{n-1}, x_n$ là chu trình Hamilton nếu $x_0, x_1,..., x_{n-1}, x_n$ là đường đi Hamilton.
- Hiểu đơn giản chu trình Hamilton là đường đi xuất phát từ một đỉnh, đi qua mọi đỉnh của đồ thị, mỗi đỉnh đúng một lần và kết thúc tại đỉnh bắt đầu.

### Ví Dụ:
Với đồ thị sau:

![đồ thị 1](/images/CS112/CompletedSearch-Backtracking/HamiltonianCycle/dothihamilton1.png)

Ta có thể tìm ra một chu trình Hamilton là: $a \to b \to f \to e \to c \to d \to a.$

![đồ thị 2](/images/CS112/CompletedSearch-Backtracking/HamiltonianCycle/dothihamilton2.png)

- **Input:** là một [ma trận kề](https://vi.wikipedia.org/wiki/Ma_tr%E1%BA%ADn_k%E1%BB%81) 2 chiều $n \times n$

$\begin{bmatrix}
   0 & 1 & 1 & 1 & 0 & 0 \\\\
   1 & 0 & 1 & 0 & 0 & 1 \\\\
   1 & 1 & 0 & 1 & 1 & 0 \\\\
   1 & 0 & 1 & 0 & 1 & 0 \\\\
   0 & 0 & 1 & 1 & 0 & 1 \\\\
   0 & 1 & 0 & 0 & 1 & 0 \\\\
\end{bmatrix}$

- **Output:** là một chu trình Hamilton (nếu có):

$\begin{bmatrix}
   0 & 1 & 5 & 4 & 2 & 3 & 0
\end{bmatrix}$

### Hướng tiếp cận:
- Sử dụng thuật toán quay lui (backtracking) với ý tưởng của thuật toán duyệt theo chiều sâu (DFS). Ta sẽ tiến hành duyệt qua đồ thị cho đến khi tất cả mọi đỉnh được thăm:
    - Bước 1: Bắt đầu duyệt đồ thị xuất phát tại một đỉnh bất kì để thăm các đỉnh kề.
    - Bước 2: Tại mỗi lần thăm ta sẽ quay ngược về đỉnh trước đó để tìm đường khác nếu đỉnh hiện tại không thể đi qua đỉnh kề nó (tức là các đỉnh lận cận đã được thăm trước đó).
    - Bước 3: Nếu chúng ta quay về được đỉnh xuất phát sau khi thăm tất cả các đỉnh của đồ thị thì đó là một chu trình Hamilton của đồ thị, ngược lại thì không tồn tại chu trình Hamilton. Lưu ý: cần phải đánh dấu mỗi đỉnh đã được thăm để không thể thăm đỉnh đó quá 1 lần.
- Minh họa quá trình giải bài toán bằng giải thuật quay lui sử dụng state-space tree:

![state-space-tree](/images/CS112/CompletedSearch-Backtracking/HamiltonianCycle/state-space-tree.png)

### Pseudo-Code:

Giải thuật bằng mã giả, sử dụng 2 hàm chính:


- Function: ``` isValid(v, k)```
- Input: Đỉnh $v$ và vị trí $k$.
- Output: Kiểm tra liệu đặt đỉnh $v$ tại vị trí $k$ có thỏa hay không.

```
    Begin
        if there is no edge between node(k-1) to v, then
            return false
        if v is already taken, then
            return false
        return true; // otherwise it is valid
    End
```
- Function: ``` cycleFound(node k)```
- Input: node của đồ thị.
- Output: return true khi có chu trình Hamilton, ngược lại return false.

```
    Begin
        if all nodes are included, then
            if there is an edge between nodes k and 0, then
                return true
            else
                return false  
        for all vertex v except starting point, do
            if isValid(v, k), then //when v is a valid edge
                add v into the path
                if cycleFound(k+1) is true, then
                    return true
                otherwise remove v from the path
        done
        return false  
    End
```



