---
layout: post
title: '3D Widget Library'
tags:
  - 3d
  - mouse-interaction
  - opengl
  - widgets

---

I've been mulling over a 3D widget library for some time. The trouble is: how does one create a widget library in the first place? I've found plenty of regular widget libraries (buttons, labels, drop-down menus, list boxes, etc.) but nothing with pizazz. I experimented with making my own using Pyglet and PyOpenGL, but those are mostly suited to making graphics, not interaction. PyMT has interaction with their widgets (as evidenced by the videos, I haven't personally gotten the code to work since I don't have a multi-touch interface), but judging from their source code, they use some simple 2D math to register whether an object was touched. I haven't yet been able to figure out how to click 3D objects with the mouse.

To make a long story short, I'm calling for help. Does anyone know of a way to make 3D graphics that respond to mouse clicks? Any other thoughts on a 3D widget library? I'd love to hear your ideas!
