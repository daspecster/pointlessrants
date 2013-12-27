---
layout: post
title: Microkernel
tags:
  - kernels
  - lines-of-code
  - linux
  - minix
  - os

---

I've been reading the MINIX textbook, which is on occasion somewhat amusing. The main focus is on microkernel OS design, the idea being that a tiny kernel is easier to maintain than a large kernel. As an example, the authors mention that MINIX 3 has about 4,000 lines of code in its kernel, which is much easier to eliminate bugs from than the millions of lines in a monolithic kernel, which makes sense.

You might think a couple of million lines of code would be impossible to maintain, and I expect you're right. How about a couple <i>hundred</i> million? Microkernels really seem like the right direction to go if this is the direction monolithic kernels are going. What do you think?
