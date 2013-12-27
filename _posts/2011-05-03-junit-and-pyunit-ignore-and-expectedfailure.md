---
layout: post
title: 'JUnit and PyUnit, @Ignore and @expectedFailure'
tags:
  - expectedfailure
  - ignore
  - java
  - junit
  - python
  - pyunit
  - unittest
  - unittesting

---

<h2>What's @ignore and @expectedFailure?</h2>
I think that JUnit's description says it best, "Sometimes you want to temporarily disable a test."

Here's the whole thing for JUnit...

<cite title="JUnit Annotation Type Ignore">"Sometimes you want to temporarily disable a test. Methods annotated with <a title="annotation in org.junit" href="http://api.dpml.net/junit/4.2/org/junit/Test.html"><code>Test</code></a> that are also annotated with <code>@Ignore</code> will not be executed as tests. Native JUnit 4 test runners should report the number of ignored tests along with the number of tests that ran and the number of tests that failed." - <a href="http://api.dpml.net/junit/4.2/org/junit/Ignore.html">http://api.dpml.net/junit/4.2/org/junit/Ignore.html</a></cite>

And for Python these two links seem to begin to explain some of the thought behind the decisions to add this feature...

<a href="http://bugs.python.org/issue1399935">http://bugs.python.org/issue1399935
</a> <a href="http://mail.python.org/pipermail/python-dev/2006-January/059503.html">http://mail.python.org/pipermail/python-dev/2006-January/059503.html</a>
<h2>My concern with this feature</h2>
I think this is one of those features that kind of got added on a slow day rather than really thinking about the impact that it has on the code and that reflection on the language. It makes sense right? You run your tests, you see some tests failing and you make a decision in your mind that you expected those to fail for a little while during development so you want them to stop sounding the alarm and blowing whistles!

This seems innocent enough at first but what are the long term implications?
Well firstly I think that you should really ask the question "Why do I have failing tests that I want to suppress??"  I can't think of any good reason personally.  If you're implementing something so huge that you've written tests that you can't make pass before you test it on an integration server then you've probably bitten off more than you can chew and your feature will change/get removed before you can make the tests pass anyway.

Secondly, writing tests should be as simple as possible. Adding something extra to a testing framework, which also defeats the purpose of the framework, seems like we're making things way more complicated than they have to be. A unittesting framework is supposed to tell you when things pass or fail. If you don't want the tests to show up as failures and they do not indicate that something is broken then remove them.

Thirdly, maintenance...who's going to clean this all up? You'll see some places that warn the users of these features about this. Make sure that you remove this before you finally commit or merge to trunk! Why not just not worry about it by not using it?

If anyone has a really great use case for this please share in the comments! I may have my opinions/rants but I'm mutable :)

Update:
<map id="imgmap2011516193348" name="imgmap2011516193348">
<area shape="rect" alt="" title="" coords="384,43,505,58" href="http://bit.ly/mt5NuR" target="_blank" />
<area shape="rect" alt="" title="" coords="65,43,186,56" href="http://bit.ly/iAXdH8" target="_blank" />
</map>
<img src="http://www.pointlessrants.com/wp-content/uploads/2011/05/twitter_expected_failure.png" usemap="imgmap2011516193348" alt="Twitter response about @ignore and @expectedFailure" />

This is an interesting perspective on the use of @expectedFailure.  Basically it can allow you to manage bugs in third-party libraries. For instance if you find a new bug in some library that your're using, you can write a test for that bug and when it gets fixed that will turn into an "unexpected success" and you can then clean up that test. 

For me I still wonder how often this is truly useful. I haven't seen a lot of tests written for bugs in third-party software. Also, if you have to use that part of the third-party library that has the bug then you must depend on that bug being there or not so you should have tests covering the outcome of the third-party's bug.
The tests that you have will be covering "your" use of the third-party software.  Obviously if the third-party software has a severe bug in it then you may decide not to continue using it.

Thanks Andrzej Krzywda! Great article on your <a href="http://andrzejonsoftware.blogspot.com/2011/05/tracking-bugs-in-external-code.html">blog</a>.
 


