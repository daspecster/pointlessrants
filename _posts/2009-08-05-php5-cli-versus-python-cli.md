---
layout: post
title: 'PHP5-CLI versus Python CLI'
tags:
  - errors
  - interface
  - php
  - python
  - tutorial

---

I just thought this was kind of interesting.   Out of the box CLI comparison of PHP and Python type errors :D
<h3>Python</h3>
<pre lang="python">&gt;&gt;&gt; test = 123
&gt;&gt;&gt; test2 = "ewfwef"
&gt;&gt;&gt; test / test2
Traceback (most recent call last):
File "&lt;stdin&gt;", line 1, in &lt;module&gt;
<strong>TypeError: unsupported operand type(s) for /: 'int' and 'str'</strong></pre>
<h3>PHP</h3>
<pre lang="php">$test = 123;
$test2 = "werwe";
echo $test/$test2;

<strong>Warning: Division by zero in Command line code on line 1</strong></pre>
It's nice that python tells you what is really wrong here, you can't divide an integer by a string! PHP on the other hand implies that $test2 is equivalent to 0.
It should be noted that python is doing a trace and PHP is not. Doing a trace on the error in PHP would give more information but since PHP is very weak with types, you would probably have to notice the error on your own.
