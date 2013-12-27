---
layout: post
title: 'HTML5 Voice Search for your blog! (Chrome only)'
tags:
  - api
  - chrome
  - google
  - html5
  - speech-recognition
  - voice-search
  - w3

---

<h2>HTML5 Voice Search How To</h2>
A while ago Google added their voice search to google.com.  This feature has been around for a while on Android and proven to be quite useful.

The HTML5 drafts have begun defining the api for voice search.

<a title="w3 draft html5 speech recognition" href="http://lists.w3.org/Archives/Public/public-xg-htmlspeech/2011Feb/att-0020/api-draft.html  ">http://lists.w3.org/Archives/Public/public-xg-htmlspeech/2011Feb/att-0020/api-draft.html</a>

If you have Google Chrome and you've tried the voice search, then you might want to add it to your site!

Believe it or not, it's really simple! I added it to this website in about 30 minutes from not knowing anything about to full implementation.
<h2>How to do it!</h2>
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
    &lt;head&gt;&lt;/head&gt;
    &lt;body&gt;
        &lt;script type="text/javascript"&gt;     
            function startSearch(event) {       
               document.getElementById("searchform").submit();     
            }   
        &lt;/script&gt;
        &lt;form action="#" method="get" id="searchform"&gt;
            &lt;input title="Search"  type="text" name="q"  x-webkit-speech="" x-webkit-grammar="builtin:search" onwebkitspeechchange="startSearch()" /&gt;
        &lt;/form&gt;
    &lt;/body&gt;
&lt;/html&gt;</pre>
<h2>More Information</h2>
<a title="Html5 Speech Voice Search" href="http://slides.html5rocks.com/#speech-input">http://slides.html5rocks.com/#speech-input</a>

<a title="W3 HTML Voice" href="http://www.w3.org/TR/xhtml+voice/">http://www.w3.org/TR/xhtml+voice/</a>

<a title="W3 HTML5 speech recognition" href="http://lists.w3.org/Archives/Public/public-xg-htmlspeech/2011Feb/att-0020/api-draft.html  ">http://lists.w3.org/Archives/Public/public-xg-htmlspeech/2011Feb/att-0020/api-draft.html</a>
