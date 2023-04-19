---
title: DOM XSS via client-side prototype pollution
date: 2023-04-19 12:17:13 +0700
categories: [PortSwigger, Prototype Pollution]
tags: [serverside, prototype_pollution]    # TAG names should always be lowercase
---

1. Nhận thấy có thể làm Object.prototype pollution bằng cách thêm một thuộc tính tùy ý thông qua URL query string. Ở đây `__proto__` sẽ trỏ đến Object.prototype và sửa đổi Object.prototype thành { "testKey": "testValue" }. Rồi đối tượng vừa được tạo ra sẽ kế thừa nó.
![image](https://user-images.githubusercontent.com/80744099/230970457-67e910c4-62fd-464b-837a-5ef076db5721.png)
2. Dùng tool DOM Invader để detect sink thì thấy sink `appendChild` trong searchLogger.js nhận giá trị transport_url để generate ra một thẻ <script> động được gán vào thuộc tính src. 
```
if(config.transport_url) {
        let script = document.createElement('script');
        script.src = config.transport_url;
        document.body.appendChild(script);
    }
```
![image](https://user-images.githubusercontent.com/80744099/230973156-677ce1ad-244f-4544-bdee-85d87e9a3592.png)
3. Chèn xss payload.