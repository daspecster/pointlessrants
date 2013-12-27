---
layout: post
title: 'Ubuntu 8.10 upgrade to 9.04 (Grub and ATI Issues)'
tags:
  - ati
  - fglrx
  - grub
  - linux
  - os
  - ubuntu
  - update

---

Well I took the plunge this weekend and upgraded my ubuntu 8.10 laptop and ubuntu 8.04 desktop to ubuntu 9.04 and I ran into two big problems.  First, my grub menu.lst wasn't updated correctly and second my ATI video drivers weren't working after the upgrade.   I'll paint a little picture of my situation just so that things all make sense.  I've did not upgrade from 8.04 to 8.10 on my desktop due to VPN PPTP issues that 8.10 was having and I really needed the VPN capability but that's all that was stopping me at the time.  I did not need the VPN functionality on my laptop so I went ahead and upgraded that machine.

My usual protocol has been to upgrade my least critical machine and test all the functionality I need and then upgrade the critical machines. So with 9.04 this is what I did as well.   My laptop had ubuntu 8.10 on it so I just clicked upgrade in the update manager and let it do it's thing.

Now if you're like me, you kind of just kept clicking "ok" on all the dialogs that popped up.  Well this is all well and good usually but in this upgrade it may have been a slight mistake.

For the grub dialogs where they ask you if you want to keep the default menu.lst, grub.lst and etc files you may want to try other options than the default.   I selected the "keep" option and I ran into some trouble.

<strong><span style="font-size: medium;">How to fix the menu.lst issue:</span></strong>

There appears to be a bug in some post-installation script that forgets to update your menu.lst correctly so I kept booting into the old version of the OS.

Firstly, I backed up my menu.lst file by doing a
<blockquote>sudo cp menu.lst menu.lst.backup</blockquote>
Then I removed the original menu.lst file. You have to completely remove the file because the update-grub script does not "update" it correctly...yes ironic I know.
<blockquote>sudo rm menu.lst</blockquote>
Next I ran the update-grub script and it searched for the installed kernels and created the correct menu.lst.
<blockquote>sudo update-grub</blockquote>
That's all it took to get it to work for me.

<strong><span style="font-size: medium;">How to fix the ATI drive issue</span></strong>

My next issue was that the ATI drivers were not working at all and xorg was just displaying rainbow colored blocks on the screen.  It was so bad in fact that I couln'd even change tty sessions (ctrl+alt + F4, F5, F6 etc...).  But I was able to ssh to my hosed machine so that's how I did the next part.

I basically did what <a title="Ubuntu 9.04 fix ATI drivers" href="https://answers.launchpad.net/ubuntu/+question/68783">this guy</a> did to get it working.

First I did the dpgk reconfigure on the xorg.conf file.
<blockquote>sudo dpkg-reconfigure -phigh xserver-xorg</blockquote>
Next I removed the FGLRX driver
<blockquote>sudo apt-get remove --purge xorg-driver-fglrx</blockquote>
Then I restarted and the screen came up but the resolution was incorrect and my dual screens wern't working.

So in the gnome menus I clicked "System"-&gt;"Administration"-&gt;"Hardware Drivers" and then enabled the video drivers from there.

After rebooting everything was working correctly, even my dual screen configuration was still there from before the upgrade.

I hope this helps some people , I know that it won't be as easy for some people as it was in my case.  Just keep working to figure it out because so far I think the upgrade is worth the trouble this time.

Also, hopefully soon I'll do a write up on converting from ext3 to ext4 because the <a title="ext3 vs ext4 benchmarks" href="http://www.linuxinsight.com/first_benchmarks_of_the_ext4_file_system.html">benchmarks(2006)</a> look awesome.
