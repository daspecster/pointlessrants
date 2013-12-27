---
layout: post
title: 'Unjustifiable Internet Explorer 7,8 and probably 9 as well'
tags:
  - bugs
  - css
  - firefox
  - internet-explorer
  - microsoft
  - web-design

---

I think we all know that Microsofts Internet Explorer has been a failure for...quite some time (Sorry Microsoft, just fix it already).  Internet Explorer 7 and 8 have made huge advances over version 6, however, there are still many flaws and I ran into an obscure one the other day.

This issue has to do with the  "text-align: justify" property.    My xhtml markup structure was something like this...
<pre>&lt;p&gt; (floated left)
     Some text in the paragraph
&lt;/p&gt;
&lt;p&gt;
     Then a bunch of paragraphs that followed
&lt;/p&gt;</pre>
So I had a single paragraph that was floated left that contained one extremely oversize character and then there were paragraphs that followed.
I also had set the paragraphs that followed to have the "text-align: justify" property.  The text was supposed to flow around the first paragraph that was floated.  This was working flawlessly in FireFox 3, but in Internet Explorer 7 and 8 it wasn't wrapping the text around the floated paragraph element.

<strong>I took out the "text-align: justify" and everything worked perfectly as it should in both Internet Explorer 7 and 8 as well as FireFox. </strong>

So Internet Explorer must have some deep philosophical issue with justified text wrapping around other objects.  This seems strange since you see that a lot in printed media.

Anyway, I hope they fix this bug before Internet Explorer 8 becomes generally available., but I doubt it.
