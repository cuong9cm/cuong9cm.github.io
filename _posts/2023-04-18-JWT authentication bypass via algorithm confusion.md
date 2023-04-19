---
title: JWT authentication bypass via algorithm confusion
date: 2023-04-18 12:12:12 +0700
categories: [PortSwigger, JSON Web Token]
tags: [serverside, jwt]    # TAG names should always be lowercase
---
1. Access vào một số standard endpoint tiềm năng. Phát hiện một json file chứa một set keys.
![image](https://user-images.githubusercontent.com/80744099/226512416-f8f04433-c60f-4abe-ac00-af250bec53f2.png)
2. Như vậy ta được biết là server sẽ sign token bằng public key RS256. Tiến hành bypass bằng cách để phía client verify alg HS256 với secret key là public key của quá trình sign token. Để làm được phải chuyển nó về định dạng phù hợp.
![image](https://user-images.githubusercontent.com/80744099/226513620-4f9c69b8-6f4c-4c08-82d2-3c3aac71c771.png)
![image](https://user-images.githubusercontent.com/80744099/226513666-591f0f9a-df15-4c94-b9c0-8a359e491a97.png)
![image](https://user-images.githubusercontent.com/80744099/226513731-3b2a88ec-93db-40c0-a309-1ef1b8f91a41.png)
3. Sửa param `alg` trong jwt thành `HS256` và `sub` thành `administrator` rồi sign một token mới với một key đối xứng mới generate
![image](https://user-images.githubusercontent.com/80744099/226515519-23429720-133f-44b6-a78d-550d70f2f547.png)