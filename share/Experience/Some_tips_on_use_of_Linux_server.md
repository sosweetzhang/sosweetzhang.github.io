---
layout: page
title: Some tips on use of Linux server
permalink: /share/Experience/231106_2/
---

<table><tr><td bgcolor=lightgray><strong>How to enable tunnel mode in "xshell" and "clash" for remote access to intranet server</strong></td></tr></table>

Configuring Clash: First, you need to make sure Clash is configured correctly and functioning properly. You need to obtain Clash's configuration file (e.g. XXX.yml), which contains the proxy server settings and rules.
- Add a configuration file in "Profiles" on the left side of Clash (drag the configuration file directly) and click to activate.
- Select "Global" in the "Proxies" on the left side of Clash and select the appropriate option below.
- In the "General" at the top of the left side of Clash, turn on "Service Mode", turn on "TUN Mode", and turn on "System Proxy".






<table><tr><td bgcolor=lightgray><strong>screen command to prevent task interruption due to disconnection</strong></td></tr></table>

<em>Here are some useful orders：</em>

_screen -S yourname -> Create a new session named yourname_

_screen -ls -> List all existing sessions_

_screen -r yourname -> Come back to the session named yourname_

_screen -d yourname -> Detach session named yourname remotely_

_screen -d -r yourname -> End the session and return to yourname session_

_screen -X -S yourname quit -> Kill the session named yourname_

<em><a href="https://www.cnblogs.com/mchina/archive/2013/01/30/2880680.html" title="">linux screen 命令详解</a> </em>


<table><tr><td bgcolor=lightgray><strong>Introduction to Nvidia-smi and description of common commands and parameters</strong></td></tr></table>

<em>Here are some useful orders：</em>

_nvidia-smi -> Show all basic information about the current GPU

_nvidia-smi -L -> List all aviliable NVIDIA devices_

<em><a href="https://blog.csdn.net/C_chuxin/article/details/82993350" title="">Nvidia-smi简介及常用指令及其参数说明</a> </em>
