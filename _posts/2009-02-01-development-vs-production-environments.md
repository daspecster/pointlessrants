---
layout: post
title: 'Development Environments vs. Production Environments'
tags:
  - arrays
  - built-in-functions
  - environments
  - objects
  - php
  - symfony

---

I like the idea of having two separate environments for my website.  That way I do not have to worry about remembering to turn off the profiler (if I'm using a profiler) or making sure that I do not mess up the database while messing around with test data etcetera.  There is also no question that <a href="http://symfony-project.org">Symfony</a> executes the Development/Test/Production environment philosophy very well.  However, there is also no question that, when one runs into a bug that only shows up in one environment and not in the other, it can be very difficult to squash, indeed.

This is what happened to me today.  I have been working on the <a href="http://www.symfony-project.org/jobeet/1_2/Propel/en/">Jobeet</a> tutorial and, on day 16, they asked me to implement an XML/JSON/YAML API module.  Of course, since it's a tutorial, they give you all the code and I was mostly just copy-pasting, but once I started poking around after completing part of the chapter, I noticed that the production environment only displayed one record while the development environment displayed (correctly) about thirty records.  I knew this wasn't right.  My first reaction was to try clearing the cache - no luck.  Now I had no idea what to do since I'm a symfony noob and the only thing that I thought was really different between production and development was that one cached and the other didn't (and the databases could be different if you wanted to set them that way, but I hadn't - it's just a tutorial, after all).

Well, to make a long story an amazing amount shorter, I went digging and found that a URL that was being generated in a loop to be used as an array key was always the same  (but only when debugging was disabled).  After some more digging, I found that the reason that it was always the same is that the method used to generate the URL was supposed to take an array as an argument and I was passing it an object instead (because the tutorial told me to).  Now here is the interesting part:  the reason this did not work was, indeed, because of caching.  It just so happens that the symfony hashing function for its URL cache uses the PHP function array_merge().  Now, I haven't looked into this in depth, but I guess when trying to merge an array and an object this function isn't the best.  However, when there is no caching enabled, the way symfony generates the URL is by using a custom function called mergeArrays:
<pre><code>
protected function mergeArrays($arr1, $arr2)
{
  foreach ($arr2 as $key =&gt; $value)
  {
    $arr1[$key] = $value;
  }

  return $arr1;
}
</code></pre>
Now, if <code>$arr1</code> were an object this wouldn't work since you can't access members of an object with the <code>[]</code> operators, but, since my object was being passed into <code>$arr2</code>, it worked fine.

The one thing I cannot decide now is if this blog post is a warning against the dangers of development vs. production environments, rewriting functions that are included in the language, dynamic languages in general, or something else I haven't thought of.  I do know I learned several things from the experience, though.  First, it's almost always my code that's wrong - not the framework.  Second, just because it works in development doesn't mean it will work in production.  And third, validate your input - if you're expecting an array, make sure it's an array and not some random object.
