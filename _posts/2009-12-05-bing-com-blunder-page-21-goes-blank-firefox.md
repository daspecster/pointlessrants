---
layout: post
title: 'Bing.com blunder: Page 21 goes blank (FireFox)'
tags:
  - bing-com
  - bug
  - firefox
  - microsoft
  - search

---

Bing.com blanks out at page 21-22 of search results in FireFox.

Take a simple search in bing.com

http://www.bing.com/search?q=ford

This will give you page saying there are 160,000,000 results and you're being shown 1-20 of them. That's all fine and dandy but let's say I want to just flip through the pages a little and see what's new with Ford.

When you click on the pagination below the URL's that your going to look something like this...

<span style="font-size: x-small;">Page 2: http://www.bing.com/search?q=ford&amp;first=6&amp;FORM=PERE</span>

<span style="font-size: x-small;">Page 3: http://www.bing.com/search?q=ford&amp;first=16&amp;FORM=PERE1</span>

<span style="font-size: x-small;">Page 4: http://www.bing.com/search?q=ford&amp;first=26&amp;FORM=PERE2</span>

<span style="font-size: x-small;">Page 5: http://www.bing.com/search?q=ford&amp;first=36&amp;FORM=PERE3</span>

You'll notice a couple things changing in these urls.  The <em>first</em> should be the "first" GET variable in the URL which appears to be some kind of page offset for the results.

The next is that FORM=PERE business which I'm not sure exactly what it does and it didn't seem to matter if I removed it from the URL anyway.

The key thing I found was that if you click through the pages until you get to around page 21 or 22 the screen goes completely blank and the magic variable value is changing "?first" to a value that's greater than or equal to 200.  This seems to only be an issue in Firefox as far as I can tell.

I checked the headers with this and there doesn't seem to be any significant differences.

<span style="font-size: x-small;">$ curl -I http://www.bing.com/search?q=ford&amp;first=16&amp;FORM=PERE4</span>

<span style="font-size: x-small;">$ curl -I http://www.bing.com/search?q=ford&amp;first=206&amp;FORM=PERE4</span>

Comment if you have any ideas?
