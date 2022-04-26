---
title: "Subset-Sum Problem"
author: Trần Phú Vinh
date: 2022-04-14T5:56:31+07:00
draft: false
tags: ["CS112"]
categories: ["Algorithms"]
math: true
---
## Đặt Vấn Đề:

Hãy tìm các tập con thuộc $A = \lbrace{a_1, a_2,..., a_n \rbrace} $ gồm $n$ số nguyên dương sao cho tổng các phần tử của từng tập con tìm được được phải bằng một số nguyên dương $d$. Để tiện lợi hơn, ta sẽ giả sử các phần tử được sắp xếp tăng dần:
            $$ a_1 < a_2 <...< a_n. $$

### Input:
- Một dãy số nguyên dương được sắp xếp tăng dần.
- Một số nguyên dương $d$.

### Output:
- Các tập con của dãy số nhập vào có tổng bằng $d$.

## Hướng tiếp cận:

### Phương pháp 1: Brute-force:
Ta có thể sử dụng brute force bằng cách tính tổng mọi tập hợp con và so sánh với $d$.

```python
from itertools import combinations

def SubSetSum(arr, d):
    for i in range(1, len(arr) + 1):
        for subset in combinations(arr, i):
            if sum(subset) == d:
                print(subset)

if __name__ == '__main__':
    array = list(map(int, input().split()))
    d = int(input())
    SubSetSum(array, d)
```
Hiển nhiên, cách tiếp cận brute force này chỉ thích hợp với input có đầu vào nhỏ. Khi kích thước mảng đầu vào tăng, số tập con mà ta phải kiểm tra với mảng có $n$ phần tử là $2^n - 1$ (không xét tập con rỗng).

### Phương pháp 2: Backtracking:

Với Backtracking, ta sẽ tạo thêm một mảng kết quả ***Result*** và luôn theo dõi tổng thay đổi như thế nào khi thêm phần tử $a_i$ vào mảng. Cách hoạt động của Backtracking được diễn tả bằng **State-Space-Tree** như sau:

**Input**
- $A = 3,5,6,7$
- $d = 15$

![State-Space-Tree](/images/CompletedSearch-Backtracking/SubSetSum/state-space-tree.png)

Ta có thể xây dựng state-space tree là một cây nhị phân với giá trị của từng nút là tổng các phần tử trong mảng ***Result***. Các nhánh bên trái là trường hợp thêm phần tử $a_i$ vào ***Result*** và ***Backtracking*** (quay lui) lại nút cha để tiếp tục tìm kiếm. Nếu $s$ không bằng $d$ thì ta sẽ bỏ nút hiện tại khi gặp một trong hai trường hợp sau:

- $s$ lớn hơn $d$ khi thêm $a_{i+1}$
            $$ s + a_{i+1} > d. $$

- Tổng $s$ và các phần tử phía sau vẫn nhỏ hơn $d$.
            $$ s +    \sum_{j = i + 1}^{n} a_j < d.  $$

## Pseudo-code:

```
    Giải thuật SubSetSum(A[], R[], sum, d):
        if sum == d:
            write R[]
            return
        else if sum > d or len(A[]) == 0:
            return
        else:
            SubSetSum(A[1..i], R[], sum, d)
            R[].append(A[0])
            SubSetSum(A[1..i], R[], sum + A[0], d)
```