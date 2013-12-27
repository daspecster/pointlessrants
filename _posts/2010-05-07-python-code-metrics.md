---
layout: post
title: 'Python code metrics'
tags:
  - code
  - complexity
  - lint
  - python

---

Recently at work I've been pushing to start tracking some metrics on our python code base. There are a few tools out there like <a title="PyGeanie code cyclomatic complexity tool" href="http://www.traceback.org/2008/03/31/measuring-cyclomatic-complexity-of-python-code/">pygenie</a>, <a title="PyChecker source code lint checker" href="http://pychecker.sourceforge.net/">pychecker</a> and <a title="Pylint lint checker for python" href="http://www.logilab.org/857">pylint</a>. These seem to be the leading code metric tools for python at the moment. Where I work we have eagerly adopted pylint in our daily use of python.

Pylint seems to be the most useful for the day to day developer. It's fast and flexible, you can run it on the file you're working in,a group of files or the entire project.

There are some problems with all of these tools when it comes to frameworks. I've been using django alot lately and with the way that it has it's settings.py file integrated it kind of  tricks these lint tools. So you may see errors saying something like this...

ImportError: Settings cannot be imported, because environment variable DJANGO_SETTINGS_MODULE is undefined.

There are a couple django-lint checkers it appears.

<a title="django-lint" href="http://github.com/lincolnloop/django-lint">django-lint</a> is a project that appears to have died. I've tried to use this a little bit, but I haven't really had much success.

It appears however that the project has moved or branched <a title="django-lint Chris Lamb" href="http://chris-lamb.co.uk/projects/django-lint/">http://chris-lamb.co.uk/projects/django-lint</a>.

I haven't tried this version but I imagine it would be better since it was last updated in March 2010.

You can also set the DJANGO_SETTINGS_MODULE environment variable like this...
<pre>$ export DJANGO_SETTINGS_MODULE=mysite.settings
$ django-admin.py runserver</pre>
<h2>So here's my story:</h2>
I have some surprising elements that came out of looking for lint tools for python or any other programming language that you're working in.

One, was that my team latched on to the pylint scoring mechanism instantly and it became a game of who could get a perfect score over all the code they were working in.  This is good for a few reasons, and I challenge those nay sayers out there.

<span style="font-size: x-small;">Warning: POINT ahead!</span>

Ok yes, maybe "your" coding style isn't accomodated in pylint...you know what! It doesn't matter.  The POINT is that everyone is meeting a STANDARD.

That's the point! I don't care if no one can get a perfect score unless all their variables start with "i" (which I assume is Apple's policy).  The power that comes with everyone driving, pushing and accelerating in the same direction is far far far more valuable than "your" coding style.
