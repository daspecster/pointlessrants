---
layout: post
title: '# Threading in Python'
tags:
  - declarations
  - python
  - threading
  - tutorials

---

<i>Henceforth all posts regarding a certain programming language shall be denoted in the title using comments specific to that language. This is for visual purposes, as well as for fun.</i>

<h3>Threading in Python</h3>

Setting up separate threads is incredibly easy in Python. There are several tutorials out there suggesting one subclass the <code>threading.Thread</code> class and override the <code>run</code> method, but this is not necessary. Simply do the following:

<pre>import threading

def func():
    # ... some code here
    pass

new_thread = threading.Thread(target=func)
new_thread.start()</pre>

This will run <code>func</code> in a new thread. Interacting threads is a bit trickier, but I refuse to write anything about that until I know something about it.
