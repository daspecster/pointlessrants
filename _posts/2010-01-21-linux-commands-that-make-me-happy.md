---
layout: post
title: 'Linux commands that make me happy'
tags:
  - linux
  - networks
  - routing
  - server
  - sudo

---

Ok, so at work I started writing a "Linux command of the day" on a whiteboard that was vacant. Some of them are pretty cool so I thought I would show them here.

Some of them are pretty elementary to linux gurus but I've been using linux almost exclusively for 2 years and some of these were new to me. This is probably because I've been using mostly gnome and am not fully dependant on the CLI.

1.  <strong>$ sudo !!</strong>
What this does is run whatever the last command you typed with sudo in front of it. Very cool, I know I've typed some long command before and forgot to add sudo to it. This makes those mistakes a lot easier to deal with. (I got this from <a title="hak5 trust your technolust" href="http://www.hak5.org">hak5.org</a>...good web show).

2. <strong>$ route  -n</strong>
I felt ashamed for not knowing this one but it will help you find what your gateway ip is.

3. <strong>$ nmap -v -O ipaddress</strong>
Ok this isn't really a build in command but if you have nmap installed this gives you a port scan and OS information from an IP address.
