---
layout: post
title: 'How To Python import GeoIP in OS X'
tags:
  - apple
  - c-libraries
  - geoip
  - install
  - maxmind
  - osx
  - python
  - usage

---

I've recently purchased a MacBook Pro and I started doing some Python/Django development. I came to a point where I had to use some of MaxMind.com's GeoIP module and setting GeoIP up on OSX was a bit more challenging than Ubuntu but it wasn't too bad.

In Ubuntu you can essentially <em>sudo apt-get install python-geoip</em> and things start working but it takes a slight bit more in OSX.

&nbsp;

In order to do this on the Mac/OS X you need to install two things,
1. The MaxMind GeoIP C library http://www.maxmind.com/app/c
<code>./configure
make
make check
make install</code>

and 2. The Python MaxMind GeoIP library http://www.maxmind.com/app/python
<code>python2 setup.py build
python2 setup.py install</code>

&nbsp;

For further information here's a great page on MaxMind.com http://www.maxmind.com/app/geoip_resources
