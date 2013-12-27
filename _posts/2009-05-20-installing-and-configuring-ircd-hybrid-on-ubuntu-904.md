---
layout: post
title: 'Installing and Configuring ircd-hybrid on Ubuntu 9.04'
tags:
  - irc
  - ircd-hybrid
  - os
  - server
  - ubuntu

---

So, the other day I was trying to setup an irc server for department communications and was having a lot of trouble getting it to accept connections from outside of localhost.  I'm using <a title="ircd-hybrid homepage" href="http://www.ircd-hybrid.org/">ircd-hybrid</a> on <a title="Ubuntu Homepage" href="http://www.ubuntu.com">Ubuntu 9.04</a> and I messed with this for hours.   I went through the ircd.conf and I kept changing the "host" parameter and different things but I finally figured out how to get the server to accept outside connections.

So I'm going to assume that you can handle all your portforwarding and networking issues, but if you have questions feel free to ask.

Step 1:
<blockquote>sudo apt-get install ircd-hybrid</blockquote>
Step 2:
<blockquote>sudo nano /etc/ircd-hybrid/ircd.conf</blockquote>
You can't tab that out because you won't have permissions to that folder.  This is good to keep your IRC secure.

Next your going to change this section...
<blockquote>listen {
/* port: the specific port to listen on.  if no host is specified
* before, it will listen on all available IPs.
*
* ports are seperated via a comma, a range may be specified using ".."
*/

/* port: listen on all available IPs, ports 6665 to 6669 */
host = "127.0.0.1";    # change this!
port = 6665 .. 6669;
};</blockquote>
To something like this...
<blockquote>listen {
/* port: the specific port to listen on.  if no host is specified
* before, it will listen on all available IPs.
*
* ports are seperated via a comma, a range may be specified using ".."
*/

/* port: listen on all available IPs, ports 6665 to 6669 */

# COMMENT OUT COMPLETELY  host = "127.0.0.1";    # change this!
port = 6667;
};</blockquote>
I've commented out the host parameter and then selected port 6667 for the listening port, which is the IRC standard.

So yeah, I know this may point out that I'm not brilliant but I tripped over it and it seemed like there was very little on the net that was of any help(maybe I should have looked harder).   But if this helps one person I will consider writing this post not a waste of my time!

Cheers everyone!
