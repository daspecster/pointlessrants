---
layout: post
title: 'The Big Permissions Scare :O'
tags:
  - authentication
  - options
  - sudo
  - usermod

---

I gave myself a pretty big scare yesterday.  I was happily going along, using my computer like usual when I started to run into some internet problems.  "Oh, I haven't changed my DNS servers today," I thought -- sometimes the DNS doesn't seem to work quite right here and I have to use OpenDNS if I want to go to any websites.  So, since I'm running Ubuntu, I opened up System-&gt;Network, clicked on Authorize, and entered my username and password.  I waited expectantly for it to authorize me, but it gave me a message that said "Error: could not authenticate,"  or something along those lines.

"Whaaaaaat?" I said aloud, to no one in particular.  My computer had been irregularly slow all day so I thought maybe something really weird was going on.  However, I had other things on my mind at the time and decided I could do without messing with it at the moment.

Later on, I decided I wanted to upgrade my packages.  I typed in <code>sudo apt-get update</code>, typed in my password, and this little gem popped up:  <code>sajo is not in the sudoers file.  This incident will be reported</code>.  "OH CRAP!" was now running through my mind.  Then it dawned on me -- I had been having some permissions problems with some command line utilities I was using the previous day (it wanted to generate files in a folder owned by "www-data") so I had added myself to the group "www-data."  I had used the <code>usermod</code> command with the <code>-G</code> option which allows one to specify a list of groups for the user.  However, when I went back to the documentation I saw that I had not read the entire explanation of the option and that in order to avoid having the command remove all the groups one was previously a part of, the <code>-a</code> option must be specified as well.  Of course, since I had stupidly not used the <code>-a</code> option, I had removed myself from the "admin" group which was my ticket into the realm of the "sudoers."

Fortunately, all I had to do was boot into recovery mode and add my user account to the appropriate groups once again, but man was I scared there for a bit.  So let this be a lesson to all - read the entire documentation for whatever command options you plan on using.
