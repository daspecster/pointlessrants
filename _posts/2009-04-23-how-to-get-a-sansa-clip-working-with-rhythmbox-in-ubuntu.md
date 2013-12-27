---
layout: post
title: 'How to get a Sansa Clip working with Rhythmbox in Ubuntu'
tags:
  - icon
  - linux
  - microsoft
  - os
  - programming
  - rhytmbox
  - sansa
  - tutorials
  - ubuntu
  - windows

---

So I got me an 8gb Sansa Clip from Walmart the other day for $50.  Yeah I know pretty decent deal for an 8gb. Anyway I was trying to get it to work with <a title="Rhythmbox Project on Gnome" href="http://projects.gnome.org/rhythmbox/">Rhythmbox</a>, and I was having some trouble but then I ran across <a title="Sansa on Ubuntu Forums" href="http://ubuntuforums.org/showthread.php?t=312196">this</a> post on Ubuntu Forums.

So apparently all you have to do in order to get the player to show up in Rhythmbox is to  <strong>add a file called ".is_audio_player" in the root directory </strong>of the Sansa MP3 player.

The root directory for me was "<em>/media/SANSA CLIP/</em>",  other files that were in this directory were the <em>MTABLE.SYS, RES_INFO.SYS</em> and <em>SYS_CONF.SYS</em>.  So that should get it to show up for you.

Also, here is a Sansa Clip Icon(right click save image as) you can put in your /usr/share/icons directory for the Sansa Clip.

<img class="alignnone size-full wp-image-386" title="Sansa Clip Icon" src="http://www.pointlessrants.com/wp-content/uploads/2009/04/clip.gif" alt="Sansa Clip Icon" />

You have to change the icon manually though, by right clicking the player once it's on your desktop.

<em>Right Click the icon for your Sansa on your desktop</em>-&gt;<em> Click  Properties</em>-&gt;<em>then next to where it says</em> "Name: " there's an icon there just click that and then you can point it to whatever icon you want.

Now you're just as cool as Vista! But actually way cooler because your OS was free :D
