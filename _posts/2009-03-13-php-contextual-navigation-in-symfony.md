---
layout: post
title: 'PHP Contextual Navigation in Symfony'
tags:
  - components
  - contextual-navigation
  - layout
  - menu
  - navigation
  - php
  - symfony

---

I am currently working on a project using <a href="http://www.symfony-project.org">symfony</a> and got to a point where I wanted to add a contextual navigation menu.  In other words, I wanted to have a menu that would show a list of pages, but not show the current page.  After considering using slots, components, and component slots, I decided on a solution that I like.  Read on to find out what it is.The concept is that I created a component to handle displaying the navigation menu and included the component in the layout.  All the component has to do is remove the current page from a list of pages that are retrieved from the global configuration file and display them as a list.  To do this, I simply created a component - you can look <a href="http://www.symfony-project.org/book/1_2/07-Inside-the-View-Layer">here</a> to find out how to do that in detail.

What it meant for me is that I created a module in my application called "navigation" (I made a folder called navigation in the modules folder) and then in the <code>navigation/actions</code> folder I created my components file:  <code>components.class.php</code>.  This is where the logic for your component goes.  Then, I created a file (partial) called <code>_navMenu.php</code> in <code>navigation/templates</code> (we'll get to why you call it that in a second) - this is the template that is displayed for the component.
<h3>The component logic</h3>
The logic for the component was as follows:
<pre><code>
// apps/app_name/modules/navigation/actions/components.class.php
class navigationComponents extends sfComponents
{
  /**
   * Executes the building of the navigation menu.
   */
  public function executeNavMenu()
  {
    $route = sfContext::getInstance()-&gt;getRouting()-&gt;getCurrentRouteName();
    $this-&gt;pages = sfConfig::get('app_navpages');
    unset($this-&gt;pages[$route]);
  }
}
</code></pre>
Basically, you're <code>components.class.php</code> file is what includes all of the components - since mine only includes one component (<code>navMenu</code>) I probably could have just had the class inherit from <code>sfComponent</code>, but I think that this may come in handy later if I ever want to add another component.  Now, the name of the method (<code>executeNavMenu</code>) is important - it determines what partial in the <code>templates</code> folder will be displayed (<code>_navMenu.php</code> - I told you we'd get to that) and it determines the name that will be used to include the component in the layout (or whatever view you may want to include the component in).  My particular component is very simple - it gets the current route (as defined in <code>routing.yml</code>) and gets a list of my possible navigation menu pages as defined in my <code>app.yml</code> file:
<pre><code>
// apps/app_name/config/app.yml - app_name is not the actual name...
all:
  .array:
    navpages:
      homepage: { name: 'Home', route: '@homepage'}
      person_index: { name: 'Manage Users', route: '@person_index' }
</code></pre>
Once I have these two bits of information, I take the item for the current route out of the list with the line <code>unset($this-&gt;pages[$route])</code>.  In my <code>routing.yml</code> file, my homepage route is defined as the following:
<pre><code>
homepage:
  url:   /
  param: { module: home, action: index }
</code></pre>
So, for example, if I am at my homepage (http://example.com/), <code>$route</code> will contain the string 'homepage' and the item with the key 'homepage' will be removed from the list.  Then, the variable <code>$pages</code> will be available in my template (partial) to be displayed.
<h3>The Component View</h3>
The code for the <code>_navMenu.php</code> partial is even more simple:
<pre><code>
&lt;div id="navigation"&gt;
  &lt;ul id="nav"&gt;
    &lt;?php foreach ($pages as $page): ?&gt;
      &lt;li&gt;&lt;?php echo link_to($page['name'], $page['route']); ?&gt;&lt;/li&gt;
    &lt;?php endforeach; ?&gt;
  &lt;/ul&gt;
&lt;/div&gt;
</code>
</pre>
In fact, it's so simple that I don't even think it needs explanation.
<h3>Including the Component in the Layout</h3>
Now all that remains is to include the component in the layout.  That can be accomplished with this one-liner:
<pre><code>
&lt;?php include_component('navigation', 'navMenu'); ?&gt;
</code></pre>
The first argument is the module in which to find the component and the second argument is the name (which I mentioned earlier) of the component itself (the name of the method minus the <code>execute</code> on the front).

As you can see, all of the individual pieces are very simple, and when you put them all together, you get a nice, logical way of building a contextual navigation menu.
