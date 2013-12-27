---
layout: post
title: 'Search Newegg with Ubiquity!'
tags:
  - firefox
  - javascript
  - ubuquity

---

This is really quite lame but it's early in the morning and I have completed my goal!

I made a <a href="http://labs.mozilla.com/2008/08/introducing-ubiquity/">Ubiquity</a> command that searches newegg for me! Yes! That is correct! *streamers, confetti and hats*

<link rel="commands" href="http://www.daspecster.com/ubiquity_commands/newegg.js" name="Search Newegg" />

The documentation that I used can be found here <a href="https://wiki.mozilla.org/Labs/Ubiquity/Ubiquity_0.1_Author_Tutorial">https://wiki.mozilla.org/Labs/Ubiquity/Ubiquity_0.1_Author_Tutorial</a>.

BONUS!: My javascript skills are a little sharper, as you can see by the complexity of the command, my skills were pretty dull to begin with :(

Here's the code incase you're too lazy to view it the easy way ;)
<pre>
<code>
CmdUtils.CreateCommand({
  name: "newegg",
  author: { name: "Thomas Schultz", email: "daspecster@gmail.com"},
  license: "GPL",
  description: "Search Newegg.com",
  help: "type newegg-search into the command line and then the phrase you want to search",
  takes: {"input": noun_arb_text},

  preview: function( pblock, input ) {
    var template = "Search Newegg for &lt;em&gt;${query}&lt;/em&gt;";
    pblock.innerHTML = CmdUtils.renderTemplate(template, {"query": input.text});
  },

  execute: function(input) {
    var searchString = escape(input.text);

    var url = "http://www.newegg.com/Product/ProductList.aspx?Submit=ENE&amp;Description=" + searchString;
    displayMessage(url);
    Utils.openUrlInBrowser(url);
  }

});
</code>
</pre>
