---
layout: post
title: 'Weird MediaWiki/Chrome Problem'
tags:
  - chrome
  - mediawiki
  - time-travel
  - troubleshooting

---

I have MediaWiki installed on my computer using Xampp. It's good for brain dumps and organizing information easily.

This evening I encountered a strange problem. For some reason, when editing the page, clicking "Save Page" doesn't make any difference to what's shown. Going back to edit, though, shows the right content, but it isn't reflected when the page is rendered. Clicking "Preview Page" will render the updated contents, but Save Page gives nothing.

It seems to be a problem with Chrome, which has been working fine with MediaWiki for months. When I loaded the wiki up in Firefox, it was rendered right and edited like it used to.

<b>Update:</b> Okay...it was clock issue. For some reason my computer set itself three hours behind. When I corrected it, the wiki worked fine, probably due to MediaWiki's version control. It was giving me the content from three hours ago (I guess).
