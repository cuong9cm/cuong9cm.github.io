## Client-side prototype pollution in third-party libraries

1. Sử dụng DOM Invader xác định được source thông qua flagment trong url

![image](https://user-images.githubusercontent.com/80744099/231079326-b20ed818-dd2d-4e81-a6f3-ac7e9b163489.png)

2. Scan gadget xác định sink setTimeout

![image](https://user-images.githubusercontent.com/80744099/231079987-94ceea80-79ca-465b-8ab1-afdd00a1f02b.png)

3. Exploit với payload
- ``#__proto__[hitCallback]=alert%281%29``

4. Craft trang exploit để chuyển hướng victim về url cùng với payload

![image](https://user-images.githubusercontent.com/80744099/231082683-e88665d1-9295-47b1-9a06-c03219d5ea21.png)
