---
title: Remote code execution via server-side prototype pollution
date: 2023-04-19 12:13:13 +0700
categories: [PortSwigger, Prototype Pollution]
tags: [serverside, prototype_pollution]    # TAG names should always be lowercase
---

1. Trong lab xác định được pollution prototype source thông qua truyền ``__proto__`` qua json request. 
2. Với account có quyền admin có chức năng chạy maintaince jobs. Khi mà kích hoạt chức năng này thì một vài tiến trình con được sinh ra.
3. Chúng ta có thể thử làm prototype pollution bằng thuộc tính execArgv với đối số --eval để sinh một quy trình con mới. Trong đó child_ process chứa phương thức execSync(), thực thi một chuỗi tùy ý dưới dạng system command.
![image](https://user-images.githubusercontent.com/80744099/232010103-c33cf884-55fd-430c-bc66-eb1520decac9.png)
4. Rồi click kích hoạt maintaince job để các tiến trình con được sinh ra trong đó bao gồm cả tiến trình xóa file morale.txt