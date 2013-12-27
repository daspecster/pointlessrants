---
layout: post
title: 'Keys to a stable application'
tags:
  - agile
  - cmmi
  - development
  - issue-tracking
  - planning
  - software
  - testing
  - unit-testing
  - waterfall

---

<h2>Unit Tests!</h2>
If you don't know about unit testing and the power and flexibility that it gives you then you NEED to get on board!
When your project has over 50% test coverage you'll start to experience a strange feeling of confidence in the code that you're writing. This confidence you're feeling will be the fact that you've seen your code perform it's duties over and over again with success.

Each time you run the tests after you've added code, you know that everything still works and that gives you huge peace of mind.

Obviously there are some other things you can aim for to aid this.

Like...
<ul>
	<li>If you find a bug...write a test that exercises it and fails...THEN fix the code and see the test pass!</li>
	<li>Aim for 80% coverage or more on the entire application.</li>
	<li>Setup hooks in your version control that runs the tests before it lets you check in your code.</li>
	<li>Use fixtures! If you interact with data then use fixtures! Do not pull from a live database! If you pull from a database on a server you're introducing configuration issues and tighter coupling.</li>
</ul>
<h3><span style="font-size: small;">Want to learn more?</span></h3>
<ul>
	<li>Wikipedia! <a href="http://en.wikipedia.org/wiki/Unit_testing">http://en.wikipedia.org/wiki/Unit_testing</a></li>
	<li>Microsoft <a href="http://msdn.microsoft.com/en-us/library/aa292197(v=vs.71).aspx">http://msdn.microsoft.com/en-us/library/aa292197(v=vs.71).aspx</a></li>
	<li><a href="http://c2.com/cgi/wiki?UnitTest">http://c2.com/cgi/wiki?UnitTest</a></li>
	<li><a href="http://docs.joomla.org/Unit_Testing">http://docs.joomla.org/Unit_Testing</a></li>
</ul>
<h2>Version Control</h2>
I didn't put this first because I assume that people use version control on their projects. If not on a RAID server or in the cloud then at least a simple Mercurial repository on their local machine.
The ability to track versions of your software is essential in providing long term stability to your application. Interestingly enough I don't think that tracking your files is what brings stability from version control. Typically when you choose some form of version control there are prescribed methods that are suggested for the developers to interact with this version control. For subversion there is the idea that you're supposed to have a "trunk" and then branch and merge back down. These methods of separation in work bring more discipline to the development of your application.

Obviously don't discount the idea of having version tracking on your source code! Version tracking has an immense value in the development of your application. Version control makes it possible to track bugs down to the very line! Version control allows you to branch your project and work on many features in parallel! Best of all version control opens the door to a world of many developers working on the application at one time!
<h3><span style="font-size: small;">Want to learn more?</span></h3>
<ul>
	<li>Good overview - <a href="http://betterexplained.com/articles/a-visual-guide-to-version-control/">http://betterexplained.com/articles/a-visual-guide-to-version-control/</a></li>
	<li>Great reviews of the leaders in version control - <a href="http://www.smashingmagazine.com/2008/09/18/the-top-7-open-source-version-control-systems/">http://www.smashingmagazine.com/2008/09/18/the-top-7-open-source-version-control-systems/</a></li>
	<li>Version control systems</li>
	<li><a href="http://subversion.tigris.org/">http://subversion.tigris.org</a></li>
	<li><a href="http://git-scm.com/">http://git-scm.com</a></li>
	<li><a href=" http://www.github.com" title="Git hosting">http://www.github.com</a></li>
	<li><a href="http://mercurial.selenic.com/">http://mercurial.selenic.com</a></li>
	<li><a href=" http://www.bitbucket.org" title="Bit Bucket Mercurial hosting">http://www.bitbucket.org</a></li>
</ul>
<h2>Best Practices</h2>
What can I say, Duh right?

If you're in school right now, tell your professor to start teaching some best practices in an area they're familiar with. You will benefit from these your entire life.
<h3><span style="font-size: small;">Want to learn more?</span></h3>
<ul>
	<li><span style="font-size: small;"><a href="http://www.google.com/search?&amp;q=programming+best+practices">http://www.google.com/search?&amp;q=programming+best+practices</a></span></li>
	<li><a href="http://en.wikipedia.org/wiki/Best_Coding_Practices">http://en.wikipedia.org/wiki/Best_Coding_Practices</a></li>
	<li><a href="http://en.wikipedia.org/wiki/Best_practice">http://en.wikipedia.org/wiki/Best_practice</a></li>
</ul>
<span style="font-size: 20px; font-weight: bold;">Testing</span>

Pretty simple, do it! Make SURE that you test your code before you commit it and send it off to your QA process. There are now quick little changes in which you don't have to test the actual user interface or consumer of your code. Do this! It's freaking annoying when you don't!

Make <span style="text-decoration: underline;">sure</span> that you have an isolated environment(integration server) to test your code on! This will make it easier and it's also very important for the next step as well.

In <a href="http://www.djangoproject.com" title="Django Python Framework">Django</a> you can even use the built in server to test your application. <a href="http://www.http://snapframework.com" title="Snap Framework written in Haskell">Snap</a>(Haskell) also has it's own server.
<h3><span style="font-size: small;">Want to learn more?</span></h3>
<ul>
	<li><span style="font-size: small;"><a href="http://www.softwareqatest.com/">http://www.softwareqatest.com</a></span></li>
	<li><span style="font-size: small;"><a href="http://www.ece.cmu.edu/~koopman/des_s99/sw_testing/">http://www.ece.cmu.edu/~koopman/des_s99/sw_testing</a></span></li>
	<li><span style="font-size: small;"><a href="http://en.wikipedia.org/wiki/Software_testing">http://en.wikipedia.org/wiki/Software_testing</a> </span></li>
</ul>
<h2>Release Planning</h2>
This is interesting because it never came up on my radar until we started doing it, and then I realized how important it really was. I mean it's obvious right? Here make this thing and then release it! Ok, how?  It's also helpful to <span style="text-decoration: underline;">practice</span> on your integration server(mentioned above) before releasing to production. This might sound silly but practice does make perfect!

Secondly, or maybe firstly, release planning just helps everyone know what their job is on release day.
<h3><span style="font-size: small;">Want to learn more?</span></h3>
<ul>
	<li><span style="font-size: small;"><a href="http://www.extremeprogramming.org/rules/planninggame.html">http://www.extremeprogramming.org/rules/planninggame.html</a></span></li>
</ul>
<h2>Issue Tracking</h2>
Ok, I'll be honest, I don't know if this goes at the top or the bottom.  You can have issue tracking setup as your developing but one thing I know for sure is that you <span style="text-decoration: underline;">need</span> it once you've released the product! Oh, and it really helps to have it public as well! Products like GetSatisfaction.com will help you communicate with your customers! And who's input should you care about the most? The people that use your product!

The trick with issue tracking is that you must respond to the issues! The quicker the better in most cases.
<h3><span style="font-size: small;">Want to learn more?</span></h3>
<ul>
	<li><span style="font-size: small;"><a href="http://en.wikipedia.org/wiki/Comparison_of_issue-tracking_systems">http://en.wikipedia.org/wiki/Comparison_of_issue-tracking_systems</a></span></li>
</ul>
<h2>Summary</h2>
The steps I've outlined here are not from any one particular process. These are just things that I've seen through trial and error that have appeared to work in my environment. I feel like they are high-level things that can be acknowledged and done that will increase the stability and maintainability of a software product.

What do you think? Feel free to comment! We can help each learn!
