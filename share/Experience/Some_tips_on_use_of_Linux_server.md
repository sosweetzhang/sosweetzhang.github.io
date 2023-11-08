---
layout: page
title: Some tips on use of Linux server
permalink: /share/Experience/231106_2/
---


<table><tr><td bgcolor=lightgray><strong>screen command to prevent task interruption due to disconnection</strong></td></tr></table>

<em>Here are some useful orders：</em>

_screen -S yourname -> 新建一个叫yourname的session_

_screen -ls -> 列出当前所有的session_

_screen -r yourname -> 回到yourname这个session_

_screen -d yourname -> 远程detach某个session_

_screen -d -r yourname -> 结束当前session并回到yourname这个session_

_screen -X -S yourname quit -> 杀死yourname这个session_

<em><a href="https://www.cnblogs.com/mchina/archive/2013/01/30/2880680.html" title="">linux screen 命令详解</a> </em>
