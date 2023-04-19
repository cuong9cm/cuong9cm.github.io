---
title: Detecting server-side prototype pollution without polluted property reflection
date: 2023-04-19 12:15:15 +0700
categories: [PortSwigger, Prototype Pollution]
tags: [serverside, prototype_pollution]    # TAG names should always be lowercase
---

1. Trong burp repeater, thử inject một thuộc tính mới cho object bằng magic method ``__proto__`` nhưng trong phản hồi lại không nhận thấy rằng inject đã thành công.
![image](https://user-images.githubusercontent.com/80744099/231974502-943bbf69-5a31-45d0-a23f-d0c9ee24200d.png)
2. Modify json request để xuất hiện lỗi syntax nhận thấy có key ``error``. 
![image](https://user-images.githubusercontent.com/80744099/231975689-e7484b68-2a8e-4c42-b176-160e9815e320.png)
3. Dùng magic method ``__proto__`` để ghi đè status code hiện tại trong `error`
```
"__proto__":{
	"status":555
}
```
3. Thì nhận thấy ta có thẻ override thành công status code bằng cách nhập sai syntax lần nữa
![image](https://user-images.githubusercontent.com/80744099/231976012-8956ab50-7206-4f44-b470-f73a9b1a1b35.png)