---
title: Làm sao để Google Chrome auto update trên Ubuntu
date: 2022-03-17T02:43:07.330Z
tags:
  - google
  - chrome
  - update
  - ubuntu
  - wget
  - apt-get
draft: false
---
First you have to install the key. This can be done by opening Terminal and typing

`wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -`

Step two is to add the repository

`sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'`

Then you update and, if you haven't already, install Google Chrome

`sudo apt-get update
sudo apt-get install google-chrome-stable`

**Phong Vân**