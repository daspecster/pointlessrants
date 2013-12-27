---
layout: post
title: 'A day with SVN CLI'
tags:
  - best-practices
  - cli
  - subversion
  - tools
  - version-control

---

<span style="font-size: large;">Problem:</span>

Have you ever seen this?
<code>
$ svn commit
svn: Commit failed (details follow):
svn: Could not use external editor to fetch
log message; consider setting the
$SVN_EDITOR environment variable or using
the --message (-m) or --file (-F) options
svn: None of the environment variables
SVN_EDITOR, VISUAL or EDITOR is set,
and no 'editor-cmd' run-time configuration
option was found
</code>

<span style="font-size: large;">Answer:</span><code>
$ export SVN_EDITOR="/usr/bin/nano"</code>

<span style="font-size: large;">Problem:</span>

I need to know what the changes I've made on my local copy?

<span style="font-size: large;">Answer:</span><code>
$ svn diff</code>

<span style="font-size: large;">Problem:</span>

You want to know what the differences are between your local copy and the repository?

<span style="font-size: large;">Answer:</span><code>
$ svn status --show-updates</code>

<span style="font-size: large;">Problem:</span>

I don't understand merges!

<span style="font-size: large;">Answer:</span>

Ok, simplest way I know how to break it down...
If you want to bring changes into your branch from the trunk, like if other people have been committing to trunk and you want their changes, simply <strong>change directories into your branch</strong> and type:
<code>
$ svn merge http://the-address-or-path-or-ssh+svn-or-svn/repositoryname
</code>

This will bring in the new changes from trunk and show you what the conflicts are, but it will not commit these updates to your branch.
Make sure that once you resolve any conflicts you do an "svn commit".

<span style="font-size: large;">Problem:</span>

I have conflicts!

<span style="font-size: large;">Answer:</span>

Well...good luck! haha jk.

First, you should notice that there is a "C" next to the list of files on the merge command that you ran.
These files should look something like filename.mine, filename.r234...etc

Step 1. What you want to do is find out which of these files has the changes that you want.
Step 2. Then, copy that file, let's say the changes we want to keep in our branch are in filename.mine, the commands would look something like...
<code>
$ cp filename.mine filename.php  (your's might not be php of course)
$ svn resolved filename.php
$ svn commit
</code>
There you've just resolved a conflict!

<span style="font-size: large;">Problem:</span>

I want to merge my awesome changes into the trunk!

<span style="font-size: large;">Answer:</span>

Step 1. "svn update" in your branch
Step 2. What you want to do is make sure that you've committed all your changes in your branch!
Step 3. Change to the trunk directory (you will need this checked out)
Step 4. "svn update" in the trunk
Step 5. "svn merge http://repository-address/repository/branches/yourbranch"
Step 6. Resolve conflicts
Step 7. "svn commit"

Ok, so I didn't say anything about trunk policy and that you should be really really careful what you put in the trunk but I'm assuming you know that!

If you want to know more about that then check out <a title="infoQ: Agile version control" href="http://www.infoq.com/articles/agile-version-control">http://www.infoq.com/articles/agile-version-control</a>

If you want to know all there is about subversion then you need to be reading <a title="SVN Book" href="http://svnbook.red-bean.com">http://svnbook.red-bean.com</a>
