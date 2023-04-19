---
title: JWT authentication bypass via jwk header injection
date: 2023-04-18 12:12:12 +0700
categories: [PortSwigger, JSON Web Token]
tags: [serverside, jwt]    # TAG names should always be lowercase
---

1. Theo đề bài, lab hỗ trợ param `jwk` để verify token. Đăng nhập với thông tin được cung cấp.
2. Trong header biết được jwt sử dụng thuật toán mã hóa RS256 = RSA + SHA-256. Ta sẽ tự tạo ra bộ public key và private key, sau đó gửi public lên. Vì trên server chỉ kiểm tra nếu có public key server sẽ sử dụng để tiến hành verify. Generate một rsa key mới trong `jwt editor keys` 
![image](https://user-images.githubusercontent.com/80744099/226249953-539a99ce-49dc-498c-ac3e-7e5e3bdda383.png)
3. Thêm claim "jwk" có giá trị là rsa key vừa generate vào header vừa sửa `sub` thành `administrator`.
![image](https://user-images.githubusercontent.com/80744099/226250170-a298e7a1-f55a-4470-a643-ad4910738b46.png)
4. Ấn attacker để embed jwk vào token. Gán giá trị jwt mới vào session cookie. Truy cập thành công tài khoản admin.
![image](https://user-images.githubusercontent.com/80744099/226250813-2bfe89ad-0db7-4741-bd1e-6d8298f1aa7d.png)
5. Vào admin panel xóa user `carlos`.