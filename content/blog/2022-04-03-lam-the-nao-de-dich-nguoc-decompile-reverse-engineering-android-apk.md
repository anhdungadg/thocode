---
title: Làm thế nào để dịch ngược (decompile, reverse engineering) Android APK
date: 2022-04-03T16:34:45.734Z
tags:
  - apktool
  - decompile
  - reverse
  - engineering
draft: false
---
<!--StartFragment-->

Có nhiều lý do để phải decompile một file APK trên Android, nếu bạn cần thì theo các bước sau đây và chỉ với 3 câu lệnh là xong.

Vì các tool này đều viết bằng Java nên đầu tiên là cài đặt Java 8, trang chủ [](https://www.java.com/en/)<https://www.java.com/en/> mấy chục năm rồi vẫn thế, chả có thay đổi gì. Trên Windows nếu cài xong mà chạy lệnh java -version không có gì thì nhớ thêm Path đến folder cài java trong System environment variables.

Xong rồi thì tải apktool về, coi hướng dẫn chi tiết trong này [](https://ibotpeaches.github.io/Apktool/install/)<https://ibotpeaches.github.io/Apktool/install/>. Không nhất thiết phải move vào C:\Windows hay /usr/local/bin chi đâu, vẫn có thể chạy lệnh apktool từ chỗ khác được.

Sau khi đã rebuild file APK bằng lệnh thì chúng ta cần sign APK này mới có thể đem cài trên thiết bị được, tải nguyên cục này về [](https://github.com/techexpertize/SignApk)<https://github.com/techexpertize/SignApk>.

**Nhiếp Phong**

<!--EndFragment-->