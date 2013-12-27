---
layout: post
title: 'Excel 2007 with Multiple Monitors'

---

I've been added as a writer to this blog for a few weeks now, but I haven't had a great idea for a first post.  I was at work today when I realized I should probably share a trick that I discovered to avoid one of my largest Microsoft pet peeves.

If you open multiple Excel files, by default the files will exist in one Excel instance.  You can't view the files on different screens.  I'm sure this saves on resources by using shared code, but I'd prefer to spend the resources for usability.  By editing the Excel file extension actions, you can change this poor behavior.

These steps assume you're using Windows XP and Excel 2007.
<ol>
	<li>Open My Computer</li>
	<li>Choose the Tools menu, then Folder Options</li>
	<li>Select the File Types tab</li>
	<li>Scroll down to XLSX and highlight it</li>
	<li>Click the Advanced button</li>
	<li>Uncheck Browse in same window</li>
	<li>Highlight the Open action and click the Edit button</li>
	<li>Make sure the Action box says &amp;Open</li>
	<li>In the Application used to perform action box, change it to contain the following: "C:\Program Files\Microsoft Office\OFFICE11\EXCEL.EXE" "%1"</li>
	<li>Check the Use DDE box</li>
	<li>Remove anything in the DDE Message and DDE Application Not Running boxes.</li>
	<li>Make sure the Application box says EXCEL</li>
	<li>Make sure the Topic box says System</li>
	<li>Click OK on all of the windows to save settings and back out</li>
</ol>
You should now be able to open two different Excel files by double-clicking on the files themselves and they won't be emprisoned in the same Excel instance.  They may start on top of each other, but you should now be able to move the windows around to different monitors individually like you would with other applications.

Keep in mind, we only did this for .xls files.  If you want this to work with other Excel file extensions, you'll need to go through the same process substituting that file extension for XLSX.  If you want this to work with Office 97-2003 files, you need to repeat the process for XLS.
