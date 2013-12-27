---
layout: post
title: 'Newegg.com design refresh critique'
tags:
  - css
  - design
  - fonts
  - html
  - newegg
  - web-design

---

<a title="NewEgg.com" href="http://www.newegg.com">Newegg.com</a> has been pretty much my exclusive site to purchase computer hardware for the last 4-5 years. Recently <a title="NewEgg.com" href="http://www.newegg.com/">Newegg.com</a> has refreshed their website design. First, I would like to say that there are some key points that I really like about the refresh.
<h3><strong><span style="font-size: large;">The good stuff...</span></strong></h3>
I want to be positive at first here, while there are some glaring mistakes I would like to focus on the good parts.

The first thing I noticed, and I mean the first, was the text for the prices (<strong>reference #5</strong>) in the list of products that you're browsing. This I really like a lot. It's cleaner and easier to read. Which I think is why I noticed it first, along with people always want to view the prices of the products they're interested in. Bravo!

Another thing I noticed, probably the second thing was that the "Compare" section had changed (<strong>reference #4</strong>). This is very nice now as well. I can see and remove the products I want to compare from this point and they carry over to the next page of products.  Very cool in my opinion. The compare page itself was cleaned up a little as well.

The page turner is kind of middle ground (<strong>reference #3</strong>). I like it but I guess it didn't really change enough for me to think it's stellar like the previous two features. One thing that did change drastically with that work flow is the "Loading..." message you get when turning pages.  I'm kind of indifferent about that as well.
<p style="text-align: center;"><a href="http://www.pointlessrants.com/wp-content/uploads/2010/03/newegg_critique.jpg"><img class="aligncenter size-full wp-image-737" title="Newegg.com Critique" src="http://www.pointlessrants.com/wp-content/uploads/2010/03/newegg_critique_thumbnail.gif" alt="Newegg.com Critique" width="650" height="296" /></a></p>

<h3><a title="Newegg.com design refresh critique" href="http://www.pointlessrants.com/2010/03/newegg-com-design-refresh-critique/"><strong><span style="font-size: large;">Ok, now for the critique part...</span></strong></a></h3>
<strong><span style="font-size: large;"><!--more--></span></strong>
<p style="text-align: center;"><img class="aligncenter size-full wp-image-739" title="W3C Validator Newegg" src="http://www.pointlessrants.com/wp-content/uploads/2010/03/newegg_w3c_validator.gif" alt="W3C Validator on newegg.com 551 errors 26 warnings" width="612" height="73" /></p>
Ok, first off I have to say...that if you run newegg.com through <a title="W3C Validator" href="http://validator.w3.org/">validator.w3.org</a> the site is quite flawed with 551 errors and 26 warnings. Now that said, I'm impressed that the page seems to display properly in my browser (ubuntu firefox 3.5).  I am kind of curious how well it looks in other browsers but I don't think I'm going to probe it that deeply.  Part of their problem here is the DOCTYPE they chose, which happens to be
<blockquote>
<pre id="line1">&lt;!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
"http://www.w3.org/TR/1999/REC-html401-19991224/loose.dtd"&gt;</pre>
</blockquote>
So while part of their problem is that they are trying to write XHTML code, they're trying to validate it against a HTML 4.01 DOCTYPE. I attempted to switch the DOCTYPE in the validator and found that there were more than double the number of errors, so at that point I gave up giving them the benefit of doubt. Seriously guys, step up your game! I know you can!

Another thing that seems strange is that the top navigation area that has dropdowns (<strong>reference #1</strong>), now seems to be very sluggish in responding to mouse movement. When you hover over them they are supposed to drop down with categories of products but this seems to take over 1.0 seconds now which is kind of aggravating to use. I don't think this is a result of my computer being slow as a few others have mentioned this to me.

Also on this note, the title links for products in the listing page used to be underlined but that has now been removed (<strong>reference #2</strong>). This I found to be quite disturbing.  Even though I've used this site for at least 4 years, I found my self hesitating to click on this text since there was no indication that it was a link. A slight color alteration here would have made some sense in my mind, but to take away all indication that this is a clickable link just doesn't add up to me.

All in all I was honestly disapointed by this update. The only really good thing I can say about it is the pricing text. I'm sure they spent thousands of dollars on this update and you would think you would at least get valid code. I don't mean to be harsh on the developers but it's really not impossible to write good XHTML markup. This problem of poor markup is pretty rampant on the internet and it's a shame to take all the work that the W3C has done and throw it away. I hope Newegg.com's next update has valid code even if that means cutting features.
