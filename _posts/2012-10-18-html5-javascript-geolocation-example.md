---
layout: post
title: 'HTML5 JavaScript GeoLocation Example'
tags:
  - api
  - code
  - example
  - geolocation
  - html5
  - javascript
  - tutorial

---

Geolocation is a very useful tool. So useful in fact that it's been added to the HTML5 specification.

What makes Gelocation so useful is how much the web is used on phone these days. Websites can now be applications on your phone. These web applications can be games, document editors, you name it!

So here's a quick intro on how to use the HTML5 Geolocation API.

{% highlight javascript %}
if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(success, error);
} else {
  error('not supported');
}
{% endhighlight %}

"success" and "error" in the getCurrentPosition() call are callback functions.

Here's an example of the success() function.
{% highlight javascript %}
function success(position) {
   document.write("Latitude: " + position.coords.latitude + " Longitude: " +     position.coords.longitude);
}
{% endhighlight %}


Here's the full example.
{% highlight javascript %}
function success(position) {
    document.write("Latitude: " + position.coords.latitude + " Longitude: " + position.coords.longitude);
}

function error(msg) {
    console.dir(msg);
    alert(msg);
}

if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(success, error);
} else {
    error('not supported');
}
{% endhighlight %}
