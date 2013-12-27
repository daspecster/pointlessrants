---
layout: post
title: 'Facebook and MySpace what lies beneath the profile'
tags:
  - facebook
  - lamp
  - myspace
  - opensource
  - presentations

---

I think most of us dabble with Myspace.com or Facebook.com to satisfy our social needs of communication.

I watched some presentations on the inner workings of Facebook.com and Myspace.com that are hosted on a cool site called infoq.com.

<strong>Myspace.com presentation by Dan Farino</strong>

<a title="InfoQ Myspace presentation" href="http://www.infoq.com/presentations/MySpace-Dan-Farino">http://www.infoq.com/presentations/MySpace-Dan-Farino</a>

<strong>Facebook.com presentation by Aditya Agarwal</strong>

<a title="InfoQ Facebook Presentation" href="http://www.infoq.com/presentations/Facebook-Software-Stack">http://www.infoq.com/presentations/Facebook-Software-Stack</a>

From these presentations I have to say that Facebook really kicks Myspace's butt. This is of course apparent when you use either site.  Facebook's backbone is a modified LAMP(Linux, Apache, MySQL, PHP) whereas Myspace is using Microsoft products like MSSQL, ASP 2.0 with some .Net 3.5 and of course Server 2003.

The Myspace presentation was mostly about maintaining the system and the tools that were created due to Microsoft's inadequate abilities to monitor it's own systems at a highly scaled level.  This presentation can be equated with the Facebook presentation as they are on different topics, however from their statements it appears that both sites had some serious issues scaling in the beginning of their existence.

One interesting thing I found was that the Myspace developers made tools to watch their own server clusters and their code was customized to only be able to be used on Myspace servers.  On the opposite side, in the creation of Facebook many <a title="Facebook open source projects" href="http://developers.facebook.com/opensource.php">new open-source projects</a> were created and can be used by many people.

Long live LAMP!  Maybe Microsoft will catch up some day.
