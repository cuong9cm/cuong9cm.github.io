---
title: JWT authentication bypass via flawed signature verification
date: 2023-04-18 12:16:12 +0700
categories: [PortSwigger, JSON Web Token]
tags: [serverside, jwt]    # TAG names should always be lowercase
---

1. Đăng nhập theo thông tin đăng nhập được cung cấp. Sau khi đăng nhập chúng ta nhận thấy một session cookie có giá trị là một JWT.
2. Dùng JWT Editor đọc được các giá trị header và payload. 
![image](https://user-images.githubusercontent.com/80744099/226193621-29e7db97-1b67-4cd2-a42b-42bafb666a10.png)
3. Trong phần header cho biết rằng signature của token được generate từ mã hóa RS256 và nhận thấy key `"sub"` có giá trị là username. Thay đổi giá trị của thuật toán mã hóa thành `none` xong đó xóa phần signarture của token và giá trị của sub là `administrator`. 
![image](https://user-images.githubusercontent.com/80744099/226194609-3e98a762-6ffa-4934-a4d8-74cc9af5c7d3.png)
4. Truy cập thành công trang admin panel. Edit cookie trong Inspect Browser để xóa user carlos
![image](https://user-images.githubusercontent.com/80744099/226194981-609cf3bb-f8bf-46ff-af53-bf791f7e40ec.png)