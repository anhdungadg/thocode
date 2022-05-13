---
title: Controller, ControllerBase, ApiController
date: 2022-05-09T10:12:27.765Z
image: /images/280346323_769963117332482_7918069011979452107_n.jpg
tags:
  - net6
  - netcore
  - controller
  - controllerbase
  - apicontroller
draft: false
---
<!--StartFragment-->

Hồi đầu nhìn thấy có vẻ giống nhau, hơi lộn lẹo nên phải biên lại đây cho dễ nhớ.

Bạn sẽ nhìn thấy 3 class này khi khởi tạo dự án WebAPI (là [ASP.NET](http://ASP.NET) Core Web API hoặc là [ASP.NET](http://ASP.NET) Web Application (.NET Framework).

Theo đó thì trên .NET Framework API sẽ như bên dưới. Muốn thay đổi route thì phải chỉnh trong App_Start/WebApiConfig.cs

`public class SampleAPIController : ApiController `\
`{`\
` // your code in here `\
`}`

Còn trên NET Core thì tiện hơn có thể set route theo từng controller hoặc từng method luôn, khá là tiện dụng với annonation method.

`[ApiController] `\
`[Router("[controller]") `\
`public class SampleAPIController : ControllerBase `\
`{ `\
`// your code in here `\
`}`

Còn Controller thì được dùng cho MVC web pages, tất nhiên rồi!

Tham khảo thêm ở đây: [](https://docs.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-6.0)<https://docs.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-6.0>

<!--EndFragment-->



Hư Trúc