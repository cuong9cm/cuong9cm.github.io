---
title: DOM XSS via an alternative prototype pollution vector
date: 2023-04-19 12:16:13 +0700
categories: [PortSwigger, Prototype Pollution]
tags: [serverside, prototype_pollution]    # TAG names should always be lowercase
---

1. Detect source bằng DOM Invader, xác định có thể pollution thông qua URL
![image](https://user-images.githubusercontent.com/80744099/231046863-3d69a621-d6bd-452e-853b-b66fd1eea6be.png)
2. Tiếp tục sử dụng DOM Invader để xác dịnh sink là hàm eval trong searchLoggerAlternative.js 
![image](https://user-images.githubusercontent.com/80744099/231047073-dbe9a934-a24c-4342-9326-c731b14c4314.png)
3. Với đoạn mã xử lý 
```
let a = manager.sequence || 1;
manager.sequence = a + 1;

eval('if(manager && manager.sequence){ manager.macro('+manager.sequence+') }');
```
4. Ta có thể hiểu là nếu thuộc tính sequence trong manager tồn tại thì nó sẽ được gán cho biến a còn nếu hông thì a có giá trị là 1. Sau đó + 1 trước khi được cho vào làm tham số của hàm evel()
- Payload:
```?__proto__.sequence=)};alert(1)//```
![image](https://user-images.githubusercontent.com/80744099/231048438-20129e88-ea9e-4af0-abc2-b8b43fafca2b.png)