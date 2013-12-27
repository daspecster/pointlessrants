---
layout: post
title: 'My Experiences with the Jaunty Jackalope'
tags:
  - '904'
  - gdm
  - jaunty
  - problems
  - ubuntu

---

I wish I could say that Ubuntu was all fun and games.  I really want to love it with all my heart, but, unfortunately, just like with any relationship, sometimes it sneaks up on you and stabs you in the back (maybe that speaks to my relationships).  For me it happened with my upgrade to the latest distribution upgrade: <a href="http://www.ubuntu.com/">Ubuntu 9.04</a>.

I started out with a working 8.04 installation.  Just as the update instructions recommended, I used the Update Manager to try to get the new version.  Unfortunately, I did not realize at first that I had not upgraded to 8.10 so I did not get the option to upgrade my distribution.  After running <code>lsb_release -a</code> I realized my mistake and changed the settings in the Update Manager (Updates-&gt;Release upgrade) to allow for "normal releases".  You see, Ubuntu distribution releases are divided into two categories: long term support releases (x.04) and normal releases (x.10).  The normal releases are not available through the Update Manager by default.

After upgrading to 8.10 I basically just booted into my desktop, went to the Update Manager and immediately started the upgrade to 9.04.  Everything appeared to go smoothly (except for some power interruptions here and there which caused me to have to re-initiate the downloading of packages), but when I booted up after the upgrade, I never got a login screen.  All I got was that stupid little twirling busy-cursor which I would be happy if I never had to set eyes on again.

At first, I suspected xorg due to some of the caveats for Intel graphics chipsets that I read about in the release notes.  I booted into recovery mode and tried running xfix to no avail.  I copied over one of my old xorg.conf backups to see if that would resolve my problems - no dice.  After that, I decided I should find out more about what was actually happening.  I opened up <code>/var/log/syslog</code> and discovered more about the source of my problems.  I was getting messages such as the following:
<pre><code>
Apr 29 09:50:02 sick-laptop gdm[5425]: WARNING: Couldn't authenticate user
Apr 29 09:50:33 sick-laptop last message repeated 25 times
</code></pre>
Then I opened up <code>/var/log/auth.log</code> and found the following:
<pre><code>
Apr 29 09:50:16 sick-laptop gdm[5425]: pam_nologin(gdm:auth): cannot determine username
Apr 29 09:50:47 sick-laptop last message repeated 27 times
Apr 29 09:51:49 sick-laptop last message repeated 51 times
</code></pre>
"Now I'm getting somewhere," I thought to myself and set off to mess with gdm configuration files and introspect my pam configuration.  I learned that gdm (gnome display manager) is the graphical login program for gnome and that pam (pluggable authentication modules) is the way authentication is handled.  I tried all kinds of stuff (fortunately I was able to access other tty sessions this entire time), but none of it seemed to work.  I posted <a href="http://ubuntuforums.org/showthread.php?p=7173815#post7173815">a question on the Ubuntu forums</a> and even submitted <a href="https://answers.launchpad.net/ubuntu/+question/69216">a bug on the Ubuntu bug-tracker</a>.  Neither of these helped me.

Finally, I came up with a solution (temporary, but a solution nonetheless).  I ran this little command from one of my tty sessions:
<pre><code>
sudo apt-get install kubuntu-desktop
</code></pre>
That's right, I installed KDE.  Kubuntu uses a different desktop display manager (kdm instead of gdm) and, fortunately, when I booted up my machine after it had installed all the necessary packages, I was able to log in no problem.  Fortunately, I don't mind KDE at all - I could definitely see myself getting used to it.  However, I suppose that, in a way, this post is a call for help.  If anyone could help me figure out my issues I would be eternally grateful.  Just look at the bug report I submitted or the question on the forums to find out more details.  I've seen that a couple of other people have/have had this problem, but so far I know of no one who has been able to solve it (without a reinstall or something similar).
