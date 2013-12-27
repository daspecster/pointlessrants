---
layout: post
title: '# Override decorator'
tags:
  - decorators
  - library
  - override
  - pyglet
  - python
  - pythonic-programming
  - tricks

---

While working with <a href="http://www.pyglet.org/">pyglet</a> one day, I made the mistake of subclassing the window class and overriding the <code>__init__</code> method, which prevented the window from showing. To fix this, it's easy enough to add a call to <code>super(Window, self).__init__(*args, **kwargs)</code>, but I went a different route. Here's a decorator called <code>override</code> that puts it in for you:

<pre>def override(function):
    def wrapper(instance, *args, **kwargs):
        super(instance.__class__, instance).__init__(*args, **kwargs)
        return function(instance, *args, **kwargs)
    return wrapper</pre>

To use it, simply use the decorator notation in a subclassed method:

<pre>class MyWindow(pyglet.window.Window):
    @override
    def __init__(self, *args, **kwargs):
        # code goes here, no need to call super!</pre>
