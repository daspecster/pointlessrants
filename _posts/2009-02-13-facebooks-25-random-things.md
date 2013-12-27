---
layout: post
title: '# Facebook''s 25 Random Things'
tags:
  - facebook
  - python
  - random

---

If you've visited Facebook in the last month, you've probably seen one of your friends lists of "25 things about me."  If you are not familiar with this latest social trend it has become quite popular to write a note on Facebook that include 25 different things about you and then tag 25 of your friends with the requirement that they fill one out themselves.  It is, as Tom says in our latest podcast (which should be up on Sunday), Facebook's version of the chain-forwarding e-mail.  After being tagged in a number of these notes, I had an idea.  I posted the following note:

<!--more-->
<blockquote>I know what you're thinking. You're thinking "Ugh, I've been tagged in another one of these random-things-about-me notes..." Trust me - this one will be different...

I must say, I feel fortunate that I have not been tagged by many people in these things (I think it's because most of my friends have at least graduated from high school), but when my MOM posted one and tagged me, I thought I'd give it a shot. This one is a little different though: these are 24 reasons I haven't done this before + 1 other comment at the end.

1. I cannot think of that many things about myself.
2. See number 9.
3. See number 22.
4. See number 17.
5. See number 18.
6. See number 21.
7. See number 24.
8. See number 20.
9. See number 11.
10. See number 14.
11. See number 16.
12. See number 8.
13. See number 3.
14. See number 6.
15. See number 23.
16. See number 5.
17. See number 10.
18. See number 13.
19. See number 7.
20. See number 4.
21. See number 15.
22. See number 12.
23. See number 19.
24. See number 1.
25. That's right, I just took you through all of 1-24 - and before you ask, no I didn't hand-craft this, I wrote a python script to do it. See, I'll do it again:
1. I cannot think of that many things about myself.
2. See number 3.
3. See number 22.
4. See number 24.
5. See number 18.
6. See number 8.
7. See number 5.
8. See number 15.
9. See number 16.
10. See number 17.
11. See number 21.
12. See number 19.
13. See number 4.
14. See number 6.
15. See number 20.
16. See number 7.
17. See number 12.
18. See number 10.
19. See number 23.
20. See number 11.
21. See number 9.
22. See number 14.
23. See number 13.
24. See number 1.
25. That's right, this one was different, but had the same effect - because numbers 2-23 really are random, haha. Here's another one:
1. I cannot think of that many things about myself.
2. See number 17.
3. See number 20.
4. See number 11.
5. See number 19.
6. See number 23.
7. See number 3.
8. See number 13.
9. See number 10.
10. See number 14.
11. See number 6.
12. See number 4.
13. See number 15.
14. See number 21.
15. See number 16.
16. See number 24.
17. See number 18.
18. See number 12.
19. See number 7.
20. See number 9.
21. See number 22.
22. See number 8.
23. See number 5.
24. See number 1.
25. I could do this all day. :P Here's the code I used:
<pre><code>
import random

numbers = range(3, 24)
random.shuffle(numbers)
final_numbers = dict()
last_number = 2

for see_number in numbers:
  final_numbers[last_number] = see_number
  last_number = see_number

final_numbers[last_number] = 24

print '1. I cannot think of that many things about myself.'

keys = final_numbers.keys()
keys.sort()

for question_number in keys:
  print '%d. See number %d.' %(question_number,\
final_numbers[question_number])

print '24. See number 1.'
</code></pre>
And here's a BONUS thing that you probably already knew about me:

I &lt;3 COMPUTERS :D</blockquote>

So yeah, I wrote a python script that basically generates a linked list.  Each number points to some number that hasn't been selected yet until all the numbers have been pointed to.  Then the last one (24) points back to 1.  I hadn't ever used Python before this and I found some great features that really helped - especially `random.shuffle()`.  Altogether, I would have to say it was much more fun than having to come up with stupid facts like, "my Mom is Canadian which means I could get dual-citizenship" or "I'm l33tS4uc3 at mini-golf."
