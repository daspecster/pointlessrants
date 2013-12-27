---
layout: post
title: 'Clojure: Where''s the Elegance?'
tags:
  - clojure
  - elegance
  - immaturity
  - truly-pointless-rants

---

I've looked at the relatively new functional programming language <a href="http://clojure.org/">Clojure</a> a bit and I have to say, I'm not impressed. Functional programming is an interesting pastime, and I'm sure it has it's uses, but when it comes to language design, it's as if the creators are deliberately going out of their way to make things difficult. 

<a href="http://www.tbray.org/ongoing/When/200x/2009/11/03/Clojure-N00b-Advice">This site</a> has a few tips for beginners, but I was especially struck by the section about namespaces, in which the author says, "There’s <code>ns</code> and <code>in-ns</code> and <code>use</code> and <code>require</code> and <code>import</code>..."

What first clued me in to some bad design ideas, however, was <a href="http://clojure.org/sequences">Clojure's sequence functions</a> (see the bottom of the page). The fact that there are 7 separate functions for getting a specific element from a sequence (<code>first</code>, <code>ffirst</code>, <code>nfirst</code>, <code>second</code>, <code>nth</code>, <code>when-first</code>, <code>last</code>) is strongly at odds with my preference for Python's there-should-be-only-one-way-to-do-it philosophy. Also, why the inconsistency of having <code>first</code> and <code>second</code> functions but no <code>third</code>, <code>fourth</code>, <code>fifth</code>, and so on? (I think we know why.) 

I know Clojure is young, but there's a difference between a language that's not mature and a language that's immature. Design features like this don't make me want to say, "Boy this is great; I can't wait 'til Clojure is more developed." It makes me want to say, "Oh grow up."

This concludes another Truly Pointless Rant.
