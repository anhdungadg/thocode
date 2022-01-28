---
title: Cài đặt Node.js phiên bản "mới nhất" trên Ubuntu WSL2
date: 2022-01-16T21:27:12.676Z
image: /images/screenshot-2022-01-22-042756.png
tags:
  - nodejs
  - wsl
  - ubuntu
  - apt
  - packagemanager
draft: false
---
Mặc định nếu cài đặt một cách truyền thống bằng lệnh sudo apt install nodejs thì chỉ có phiên bản 10.x, lý do vì đây là phiên bản “mới nhất” là thằng package manager apt này có được.

Trong khi hiện tại, trên trang chủ thì bản LTS là 16.x, có nhiều cách để cài bản mới nhất thiệt sự từ trang chủ, và đây là một trong những cách dễ nhất:

`cd ~`

`curl -sL`[`https://deb.nodesource.com/setup_16.x`](https://deb.nodesource.com/setup_16.x)`-o nodesource_setup.sh`

`sudo bash nodesource_setup.sh`

`sudo apt install nodejs`

Xong, chỉ vậy thôi! Để kiểm tra coi phiên bản nào thì chạy

`node -v`