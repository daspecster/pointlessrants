---
layout: post
title: '# OpenGL in Python'
tags:
  - ez_install
  - graphics
  - opengl
  - performance
  - pyopengl
  - python

---

Somebody has worked out an <a href="http://pyopengl.sourceforge.net/">OpenGL wrapper for Python</a>. The installation steps are <a>here</a>, but I found them a bit non-trivial. Here's what it will take to get going.

<!--more--><h3>Getting PyOpenGL</h3>

A very useful script is <a>ez_setup.py</a>. Copy the text from that page to a new .py file. Save it as "ez_setup.py" and run it. I use the Windows command line to run Python programs, so I would type <code>python ez_setup.py</code>. 

In order to actually install PyOpenGL, however, you have to run the 'easy_install' executable found in your Python scripts directory. Move to 'C:Python25Scripts' in the command line. Type <code>easy_install PyOpenGL</code>. This should start downloading and installing PyOpenGL, though I had some trouble the first time (it may have been due to using Python 3 rather than 2.5).

<h3>Using PyOpenGL</h3>

In your favorite Python editor (I use <a>Notepad++</a>), make a new Python file and start off with this:

<pre>from OpenGL.GL import *
from OpenGL.GLU import *
from OpenGL.GLUT import *</pre>

This will import all the variables and functions from GL, GLU, and GLUT. Using <code>from ... import *</code> in Python is not generally recommended, since it imports everything from a module and undoes the namespace functionality Pythonistas prefer. However, OpenGL prefaces all its functions and variables with 'gl', 'glu', or 'glut' accordingly. It would be redundant to type 'gl.glVertex(...)', so importing everything is permissible when using OpenGL.

If you have any experience with OpenGL, you can use it more or less the same what it is used in C or C++. PyOpenGL is a wrapper written by hand, so there are some subtle differences between the standard OpenGL and PyOpenGL. For instance, I have run into problems with the use of glColorf(...). PyOpenGL does not have the function, and instead uses glColor(...), which makes sense since Python is dynamically typed.

If you don't have experience with OpenGL, <a>NeHe</a> is a good place to start. Also, I got some good out of this <a>PDF</a>.

<h3>Improving Performance</h3>

A commenter in <a>this thread</a> seems to think that PyOpenGL is somewhat slow, and his recommendation is to write the OpenGL calls in a C file and compile it into a .dll file that can be used in Python. The OpenGL code between C and Python is virtually identical (except for some variable type issues as mentioned above). I haven't tried this personally, since I'm experimenting right now, but once I get things working the way I want, I'll probably give it a shot.

