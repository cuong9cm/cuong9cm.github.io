---
title: JWT authentication bypass via weak signing key
date: 2023-04-18 12:17:12 +0700
categories: [PortSwigger, JSON Web Token]
tags: [serverside, jwt]    # TAG names should always be lowercase
---

1. Brute-force secret key bằng hashcat với wordlist các secret key phổ biến.
![image](https://user-images.githubusercontent.com/80744099/226288147-e08e2467-9fdb-4616-b910-0de029a76146.png)
3. Generate New Symmetric Key với giá trị của claim `k` = giá trị Encode Base64 của `secret1`. 
4. Sau đó resign lại jwt trong tab jwt repeater
![image](https://user-images.githubusercontent.com/80744099/226291599-cbf11525-cf32-4a6d-892b-2208718f8c3e.png)