---
title: Privilege escalation via server-side prototype pollution
date: 2023-04-19 12:18:13 +0700
categories: [PortSwigger, Prototype Pollution]
tags: [serverside, prototype_pollution]    # TAG names should always be lowercase
---

1. Sau khi đăng nhặp vào tài khoản wiener được cập. Nhận thấy chức năng update thông tin nhận vào một chuỗi json và trả lại cũng là một chuỗi json. 
![image](https://user-images.githubusercontent.com/80744099/231103891-90f15b68-dcc0-48b7-ab1b-ff1ab70847be.png)
2. Ở đây xuất hiện key `isAdmin` để xác thực đối tượng có phải admin không. Ta sẽ gọi đến magic method `__proto__` để nó trỏ đến prototype của object đang chứa nó, có thể là User Object rồi append trường `isAdmin = true` cho nó. Nhận thấy response trả về đúng như mong đợi
![image](https://user-images.githubusercontent.com/80744099/231104806-a8cc53f5-1d27-48b9-899e-cb7d8eaaced4.png)
3. Reload lại trang thì xuất hiện admin panel -> leo quyền thành công
![image](https://user-images.githubusercontent.com/80744099/231105014-12f808c1-a8f0-4bec-a845-34295a672a12.png)