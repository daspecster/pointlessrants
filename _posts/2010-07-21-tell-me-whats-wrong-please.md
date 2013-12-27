---
layout: post
title: 'Tell Me What''s Wrong, Please'
tags:
  - error-messages
  - microsoft
  - sql-server-2008

---

<p>
I recently finished college - graduated in May - and started working at my first job.  I have now officially been a developer at <a href="http://www.sonomapartners.com/">Sonoma Partners</a> for two weeks.
</p>
<p>
Due to the fact that I like Linux and open source software in general, it has been a bit of an adjustment to transition to a place where almost every tool or technology I use is provided by Microsoft (Sonoma Partners is a Microsoft partner which sells, customizes, and provides consulting services for Microsoft Dynamics CRM software).  Some might say that I have sold out to the man (in fact, several people already have), but I figure that as long as <i>I</i> am not paying for Microsoft software, I have no problem using it.</p>
<p>
At least, that's what I was thinking when I accepted the position.  For the most part I still feel that way, but lately it seems like I've been spending a ridiculous amount of time troubleshooting installation/configuration errors and not very much time actually doing useful stuff.  It's not even the errors that I've been getting that I really have a problem with - it's the error messages.  If my software messes up, I would like it to at least tell me what happened that made things go wrong.</p>
<p>
Here is an example of an error message that I got (after searching through the log - the original message just told me that my login failed) using Microsoft SQL Server 2008 yesterday: </p>
<pre>
<code>
Error: 18456, Severity: 14, State: 11.
Login failed for user 'DOMAIN\user'. Reason: Token-based server access validation failed with an infrastructure error. Check for previous errors. [CLIENT: ]
</code></pre>
<p>
Now, that seems straightforward enough, except that it says something about an infrastructure error, which made me think that something with the actual application went wrong, not just that I have the wrong login.  Furthermore, when I checked on that "State: 11" business, I found that it means "Valid login but server access failure" (<a href="http://blogs.msdn.com/b/sql_protocols/archive/2006/02/21/536201.aspx">see here for reference</a>). That made me think that something was wrong with my attempts to access the server, as well.
</p>
<p>
After a bunch of troubleshooting, I finally found out that it wasn't any sort of strange problem, but rather a case of my Windows Authentication account not being a user in the database instance.  All I had to do to fix my problem was start the database instance in single-user mode (by adding "-m" to the start-up parameters, <a href="http://blogs.msdn.com/b/raulga/archive/2007/07/12/disaster-recovery-what-to-do-when-the-sa-account-password-is-lost-in-sql-server-2005.aspx">see here for details</a>), make sure that there were no other programs running that were connecting to the database instance, and add myself as a user.</p>
<p>
So yeah, Microsoft, I'd like to see some better error messages.  Why can't you tell me that that user doesn't exist in the database?  That would be fantastic - please don't give me this crap about it being for security reasons.</p>
<p>
To see the forum thread that finally got me on the right track, <a href="http://social.msdn.microsoft.com/Forums/en-US/sqldatabaseengine/thread/8aede8b7-f314-478c-a1fe-8c30597fd0b3/#818b5588-ec23-4797-ae70-d22161474488">go here</a>.</p>
