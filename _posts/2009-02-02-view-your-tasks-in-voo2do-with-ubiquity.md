---
layout: post
title: 'View Your tasks in Voo2do with Ubiquity'
tags:
  - javascript
  - jquery
  - ubiquity
  - voo2do

---

OK, Tom officially got me hooked.  After his little blog post about Ubiquity and writing a command, I had to check it out for myself.  It wasn't too hard to get an idea - I use a handy little web-site called <a href="http://voo2do.com">voo2do</a> and I've been thinking about messing with their API for a while.  Well, now I got my chance.<!--more--> I wrote a simple little Ubiquity script to show you your pending tasks and learned a LOT in the process!  Currently, you have to be logged in for it to work (otherwise it will just tell you you've got "0" tasks pending).  Here's the code:
<pre><code>
CmdUtils.CreateCommand({
  name: "view-tasks",
  homepage: "http://stevenoxley.blogspot.com/",
  author: { name: "Steven Oxley", email: "steven.aj.oxley at gmail.com"},
  contributors: ["Steven Oxley"],
  license: "GPL",
  description: "Looks up your pending tasks on the website at http://voo2do.com.",
  help: "You can wait to see a list of your tasks in the preview area or hit enter to go to the voo2do website.",

  preview: function( pblock ) {
  	var template =  "&lt;i&gt;You have &lt;b&gt;${tasks.length}&lt;/b&gt; tasks pending.&lt;/i&gt;" +
		"&lt;ul&gt;" +
        	    "{for task in tasks}" +
			"{if typeof task == \"object\"}" +
				"&lt;li&gt;${task.getAttribute(\"taskdesc\")}&lt;/li&gt;" +
			"{/if}" +
		    "{forelse}" +
			"&lt;li&gt;You don't have any pending tasks&lt;/li&gt;" +
		    "{/for}" +
		"&lt;/ul&gt;";
    pblock.innerHTML = "Views your pending Voo2do tasks";
  	  this._getTasks( pblock, template );
  },

  _getTasks: function( previewBlock, template ) {
  	var baseUrl = "http://voo2do.com/api/getIncompleteTasks";
    CmdUtils.previewGet( previewBlock, baseUrl, function( returnedTasks ) {
      var tasklist = returnedTasks.getElementsByTagName("task");
      previewBlock.innerHTML =
            CmdUtils.renderTemplate( template, {tasks: tasklist} );
    })
  },

  execute: function() {
  	var url = "http://voo2do.com/tasks";
  	Utils.openUrlInBrowser(url);
  }
});
</code></pre>
And here is my subscriptions page if you have any desire to subscribe to this particular Ubiquity command:  <a href="http://www.andrews.edu/~sajo/ubiquity-scripts/">http://www.andrews.edu/~sajo/ubiquity-scripts/</a>.  Try it for yourself, it's fun!
