---
title: Some tricks with NET 6.0
date: 2022-05-06T05:29:00.170Z
image: ""
tags:
  - netcore
  - net6
  - dotnet
  - visualstudio
draft: false
---
IDE: Visual Studio 2022

# Hide Warning Code

Open .csproject file, add this line below into the `<PropertyGroup>`

`<NoWarn>$(NoWarn);1591</NoWarn>`

In there: 1591 is the Code show in Error List

![](/images/screenshot-2022-05-06-123556.png)



**Hư Trúc**