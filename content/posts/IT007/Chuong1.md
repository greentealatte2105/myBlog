---
title: "Tổng Quan Về Hệ Điều Hành"
author: Lê Trần Hữu Phước
date: 2022-04-28T10:12:39+07:00
draft: false
math: true
tags: ["IT007"]
categories: ["Operating System"]
---

Hệ Điều Hành (Operating System) là một **chương trình** dùng để quản lý các **phần cứng máy tính**. Hệ điều hành cũng cung cấp nền tảng cho các chương trình ứng dụng và đóng vai trò như một **người trung gian** giữa người dùng (user) và phần cứng máy tính (computer hardware). 

Trước khi đi vào chi tiết của hệ điều hành, ta cần phải biết vài thứ về **cấu trúc hệ thống** (system structure). Vì thế, trong bài viết này và những bài tiếp theo, ta sẽ thảo luận về các chức năng cơ bản như khởi động hệ thống (system startup), các thiết bị nhập xuất (I/O), và bộ nhớ. Ngoài ra, còn có các kiến thức liên quan như: cấu trúc dữ liệu dùng trong hệ điều hành, môi trường tính toán (computing enviroment) và một số hệ điều hành mã nguồn mở.

## Hệ Điều Hành làm những công việc gì?
Ta sẽ bắt đầu bằng việc xem xét vai trò của hệ điều hành trong toàn bộ hệ thống máy tính:

Hệ thống máy tính (computer system) thường được chia thành 4 phần chính: 
- **Phần cứng (hardware):** (như CPU, memory, thiết bị I/O), cung cấp tài nguyên tính toán cho hệ thống.
- **Hệ điều hành (OS):** điều khiển phần cứng và hòa hợp tiện ích giữa các **chương trình ứng dụng** để giải quyết vấn đề tính toán của người dùng (user).
- **Chương trình ứng dụng:** (như word processor, spreadsheet, trình duyệt web) phân chia thích hợp cách sử dụng các tài nguyên.
- **Users:** người sử dụng các chương trình ứng dụng để giải quyết vấn đề.

![Abstract view of the components of a computer system](/images/IT007/Abstract_view_of_comp_sys.png)
Hình 1.1: Abstract view of the components of a computer system

Ngoài ra, ta có thể xem hệ thống máy tính gồm: phần cứng, phần mềm và dữ liệu. Hệ điều hành là nơi cung cấp phương tiện cho các tài nguyên sử dụng khi hệ thống máy tính vận hành. Để dễ hình dung hơn, ta sẽ xem hệ điều hành như **government**, nghĩa là bản thân nó không cung cấp bất kỳ một chức năng nào, nó chỉ đơn giản là cung cấp môi trường cho các chương trình ứng dụng khác làm việc.

Để hiểu rõ hơn nữa về vai trò của hệ điều hành, ta sẽ cùng nhau xem xét nó dưới góc nhìn của [*người dùng*](#từ-góc-nhìn-của-người-dùng-user-view) và [*hệ thống*](#từ-góc-nhìn-hệ-thống-system-view).

### Từ góc nhìn của người dùng (User View):

Đối với người dùng, phần lớn sẽ phụ thuộc vào **giao diện** mà họ sử dụng:
- **PC (personal computer):** gồm màn hình, bàn phím, chuột và system unit, hệ thống của PC sẽ được ưu tiên thiết kế dành cho **một user** sử dụng toàn bộ tài nguyên. Mục tiêu là tối đa hóa công việc user cần giải quyết. Nên trong trường hợp này, hệ điều hành sẽ được thiết kế sao cho có giao diện *dễ sử dụng nhất*.
- **Mainframe:** user sẽ ngồi tại mỗi **terminal** và kết nối đến **mainframe**. Những user sẽ chia sẻ tài nguyên và trao đổi thông tin lẫn nhau. Hệ điều hành lúc này sẽ được ưu tiên thiết kế cho việc tối đa hóa việc sử dụng các tài nguyên - đảm bảo rằng các yếu tố như thời gian có sẵn của CPU, bộ nhớ và I/O được sử dụng một cách *hiệu quả nhất.*

![Mainframe](/images/IT007/mainframe-interview-questions-q1.png)

- **Workstation**: Người dùng ngồi tại workstaion và kết nối đến mạng của các workstation khác và các server. Người dùng tại trường hợp này vừa toàn quyền sử dụng tài nguyên của họ vừa chia sẻ các tài nguyên như tệp tin. Nên hệ điều hành cần phải thỏa mãn cả hai yếu tố đó là *dễ sử dụng* và *tận dụng tài nguyên một cách hợp lý.*

Ngoài những trường hợp phổ biến đã nêu trên, một vài máy tính hầu như không có góc nhìn của người dùng (user view). Ví dụ, máy tính nhúng (embedded computer) dùng cho trong các thiết bị nhà ở hay xe ô tô, chúng thường chỉ có các nút bấm hay công tắc chỉ để hiện thị trạng thái hoạt động của thiết bị, tuy nhiên bản thân nó và hệ điều hành của chúng chủ yếu tập trung vào việc vận hành mà không có sự can thiệp của người dùng.

### Từ góc nhìn hệ thống (System View):
Như ta có thể thấy từ [góc nhìn người dùng](#từ-góc-nhìn-của-người-dùng-user-view), hệ điều hành là một chương trình có liên quan mật thiết nhất đối với các tài nguyên (hay phần cứng). Trong ngữ cảnh này, ta có thể xem hệ điều hành như một **người phân phối tài nguyên**. Để giải quyết các vấn đề tính toán, hệ thống máy tính cần dùng đến các tài nguyên như: thời gian CPU, không gian bộ nhớ, không gian lưu trữ tệp tin, các thiết bị nhập xuất,... Hệ điều hành có nhiệm vụ quản lý các tài nguyên này.

Tuy nhiên, khi phải xử lý nhiều yêu cầu và có thể dẫn đến xung đột, hệ điều hành cần phải đưa ra quyết định để phân bố các nguồn tài nguyên một cách hợp lý và hiệu quả. Như đã biết ở phần trên, việc phân bố tài nguyên hợp lý rất quan trọng khi người dùng (user) kết nối đến cùng một *mainframe* hay *minicomputer*.

## Kết luận:
Đến bây giờ, hy vọng bạn sẽ hình dung ra được khái niệm **Hệ Điều Hành** là gì? 

Như các bạn đã thấy, chúng ta không có một định nghĩa hoàn toàn đầy đủ cho khái niệm này thay vào đó nó sẽ phụ thuộc vào từng trường hợp khác nhau. Chương trình hệ điều hành tồn tại đơn giản bởi vì chúng cho ta một phương pháp hợp lý để giải quyết vấn đề trong các hệ thống tính toán (computing system). Mục tiêu chung của chương trình hệ điều hành là giúp thực thi chương trình phục vụ cho việc người dùng giải quyết vấn đề dễ dàng hơn.

