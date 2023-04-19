---
title: JWT authentication bypass via jku header injection
date: 2023-04-18 12:13:12 +0700
categories: [PortSwigger, JSON Web Token]
tags: [serverside, jwt]    # TAG names should always be lowercase
---

1. Trong header của token biết được token sử dụng thuật toán mã hóa RS256. 
2. Site hỗ trợ `jku` param với giá trị trỏ đến url chứa các key được sử dụng để verify signature. Craft trang exploit server thành 1 file JSON có giá trị là các public key RSA được generate bằng jwt extension.
![image](https://user-images.githubusercontent.com/80744099/226392983-065400f4-2bc9-4c3a-979a-deb6df028d49.png)
3. Thêm `jku` có giá trị = url exploit server và `sub` thành `administrator`. Rồi resign lại signature với rsa key mới generate. (cần `kid` param giống nhau)
![image](https://user-images.githubusercontent.com/80744099/226394499-dcf35b1e-4db5-4853-b290-0bbee58ba58c.png)
4. Vào admin panel xóa user `carlso`
![image](https://user-images.githubusercontent.com/80744099/226397718-5ea53b7d-e84b-4a79-94df-6510f72de7a2.png)