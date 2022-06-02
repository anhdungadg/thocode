---
title: Làm sao để publish package lên Nuget.org
date: 2022-06-02T06:55:14.322Z
tags:
  - net
  - framework
  - nuget
  - package
draft: false
---
# 1. Nuget là gì?

Đã có người trả lời câu hỏi này rồi, nên bạn cứ coi ở đây: [https://anhdung.me/2015/04/02/nuget-la-gi/ ](https://anhdung.me/2015/04/02/nuget-la-gi/)

Thật ra, nếu mà bạn không biết [Nuget là gì](https://anhdung.me/2015/04/02/nuget-la-gi/) thì chắc cũng không cần phải coi thêm mấy bước sau chi nữa đâu.

# 2. Đăng ký tài khoản trên nuget.org

Vào <https://www.nuget.org/> là xong thôi. Nuget hiện chỉ cần có Microsoft account (chẳng hạn như Office 365, các dịch vụ mail xưa nay hotmail/ outlook/ live) là có thể Signin vô được.

Signin vô được rồi thì click vô account name của mình, chọn mục API Keys rồi click Create để tạo key. Tạo xong nhớ copy để xuống bước 3 mình có mình xài nghen.

# 3. Build code và publish

Cứ làm cái gì mình thích, bên dưới là một vài thứ hay ho bạn có thể thêm vào trong file csproj để hiển thị khi publish lên Nuget. Trong đó thuộc tính GenerateDocumentationFile sẽ cho phép giữ nguyên thông tin comment không bị mất.

<Description>My Awesome Package<Description/>
<GenerateDocumentationFile>true</GenerateDocumentationFile>
<PackageId>AwesomePackage</PackageId>
<Version>1.0.0</Version>
<Authors>Fun Corp</Authors>
<Company>Fun Inc</Company>

Sau khi xong xuôi thì Build lại project thử, build xong thì Pack. Giờ đây trong thư mục bin/Debug sẽ xuất hiện thêm file xxx.version.nupkg, đây chính là file bạn cần publish lên.

Giờ mở terminal lên, cd vô ngay thư mục vừa tạo ra file nupkg hồi nãy.

dotnet nuget push xxx.version.nupkg --api-key \[key hồi này mới copy] --source https://api.nuget.org/v3/index.json

# 4. Xong

Vô lại nuget.org chọn Manage Packages rồi coi package đã được duyệt và listed chưa. Trong này cũng có nhiều chỗ hay ho như là update lại thông tin Readme, bla bla bla...

**Hư Trúc**