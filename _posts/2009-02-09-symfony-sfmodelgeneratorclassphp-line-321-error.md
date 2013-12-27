---
layout: post
title: 'Symfony sfModelGenerator.class.php line 321 error'
tags:
  - code
  - error
  - php
  - symfony

---

Well I've been playing with <a href="http://www.symfony-project.org">Symfony</a> and I started building modules today from the <a href="http://www.symfony-project.org/jobeet/1_2/Propel/en/03">Jobeet day 3 tutorial</a> and I ran into an issue.   The Symfony Project is basically a framework in which you can build PHP web applications which I've been using for a school project.

I'm not sure if I missed a step of if this is a system specific problem but basically I went to run the "symfony propel:build-module" command to genereate my module files and I got this error.
<blockquote>Fatal error: Class 'PersonForm' not found in /var/www/cam/trunk/lib/generator/sfModelGenerator.class.php on line 321</blockquote>
The "PersonForm" class was, as the error indicated, no where to be found.  It turned out that I needed to run the command "<strong>symfony cc</strong>" which clears the symfony cache of files.   I also had to run the command "<strong>symfony propel:build-forms</strong>"  in order to get symfony to build my modules.

So to re-cap
<ol>
	<li>Run $ php symfony cc</li>
	<li>Run $ php symfony propel:build-forms</li>
	<li>Run $ php symfony build:module  (Params)</li>
</ol>
Once I did those steps the build:module step worked perfectly and I was able to view the skeleton application at my dev.php/person url.

Symfony seems to be very very powerful and I'm excited to learn how to develope applications with it.
