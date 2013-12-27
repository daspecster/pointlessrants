---
layout: post
title: 'Balthasar Week 2 Report'
tags:
  - balthasar
  - google-groups
  - googlecode
  - opengl
  - pyglet
  - python
  - twitter
  - widget-library

---

In a <a href="http://www.daspecster.com/2009/09/myth-of-the-genius-programmer/">post</a> a couple of weeks ago, I mentioned setting up a new GoogleCode project. I'm happy to say that <a href="http://code.google.com/p/balthasar/">Balthasar</a> is coming along nicely. For details on what Balthasar is and how to get involved, read on.

<h1>Background</h1>

I'd been hunting around for a widget library that would let me do stuff in 3D, but without luck. I knew OpenGL could do some things, but trouble picking objects with the mouse created roadblocks. Persistence, though, actually does pay off. Using <a href="http://www.pyglet.org/">Pyglet</a>, I've built a library for interacting with 3D objects. I call it Balthasar, named after the turtle that lives in our kitchen sink, whose was named, in turn, after a <a href="http://ursulav.deviantart.com/art/Balthazar-Disdains-The-Lemon-10396432">judgmental terrapin</a>.

<h1>What It Does</h1>

Right now features are sparse, but that's not to say it can't do some very important things. In fact, I got bogged down this week trying to get panning over a 3D scene to work intuitively. I can't say it's perfect yet, but it's much better than earlier attempts and good enough to leave be for now. On the other hand, orbiting the camera around its target works brilliantly! (I've never found spherical coordinates to be so useful.)

The other major feature from the client's perspective is the ability to create Widgets, 3D objects that can be selected. One nice thing is the ability to load .obj files, meaning one can (currently) create widgets of whatever size and shape in a program like <a href="http://www.blender.org/">Blender</a>, export them as .obj files, then load them in a Balthasar app. This is significant since one of my big motivations is boredom with the plainness of standard widget libraries.

From the client side of Balthasar, there seem to be quite a few decorators. They're used for changing an application's event handlers and add drawing routines to the list of things to draw.

<h1>Examples</h1>

I've had a few applications in mind that I've wanted to make, and I'm developing them using Balthasar. The examples are a major driving force behind improvements to Balthasar's library and client interface. So far the only example is <code>solar</code>, a solar system simulator based on actual planetary data. Because I wanted to be able to move around within the scene, camera orbiting and panning became important. Thus, those features are now in Balthasar.

I'll be developing a few other applications as well, hopefully developing the <i>widget</i> part of 'widget library'. I'll include them in the trunk under <code>examples</code>.

<h1>Getting Involved</h1>

There are a few ways to get involved with the project. One way is the <a href="http://groups.google.com/group/balthasarproject">Google Groups discussion</a>. Another is on <a href="http://twitter.com/">Twitter</a>, where I've started using the <a href="http://twitter.com/#search?q=%23balthasar">#balthasar</a> hashtag when I make comments about the project. If you have any interest, I'd be happy to have your help, so drop me a line if you want to know more.
