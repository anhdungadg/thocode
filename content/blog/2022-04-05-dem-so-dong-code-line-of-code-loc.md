---
title: Đếm số dòng code (Line of Code, LOC)
date: 2022-04-05T02:03:25.014Z
tags:
  - loc
  - line
  - code
  - count
  - analyze
draft: false
---
Nếu xài Visual Studio thì có cái tool Calculate Code Metrics trong menu Analyze.

Hoặc không thì mở Power Shell lên cd vô folder cần đếm rồi chạy, nhớ thêm/ xóa mấy cái file ext cần thiết nha.

***(gci -include .cs,.xaml,.js,.cshtml -recurse | select-string .).Count***