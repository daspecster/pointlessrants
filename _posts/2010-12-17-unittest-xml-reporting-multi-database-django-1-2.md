---
layout: post
title: 'unittest-xml-reporting multi database django 1.2'
tags:
  - continuous-integration
  - git
  - hudson
  - junit
  - python
  - unit-testing
  - xml

---

<h3>Background</h3>
I've recently started playing with continuous integration platforms like <a title="Hudson Continuous Integration" href="http://hudson-ci.org/">hudson</a> and <a title="Cruise Control" href="http://cruisecontrol.sourceforge.net/">cruise control</a>.  Currently most of my projects are written in python using django. There's just one problem...The django unit test runner doesn't output XML. These continuous integration platforms need JUnit XML output so that they can parse the test results.

There are a few test runner projects out there that seems pretty good. I haven't seen any yet that support the XML output and multiple databases in django(there could be some, I didn't look super far).
<h3>What I did</h3>
I forked danielfm's project(<a href="https://github.com/danielfm/unittest-xml-reporting">https://github.com/danielfm/unittest-xml-reporting</a>) and updated the run_tests() function and converted it to the new django 1.2 class for TEST_RUNNERS.

This article on django test runners explains the change pretty clearly <a href="http://docs.djangoproject.com/en/dev/topics/testing/?from=olddocs#defining-a-test-runner">http://docs.djangoproject.com/en/dev/topics/testing/?from=olddocs#defining-a-test-runner</a>.
<blockquote>Changed in Django 1.2: Prior to 1.2, test runners were a single function, not a class.
A test runner is a class defining a run_tests() method. Django ships with a DjangoTestSuiteRunner class that defines the default Django testing behavior. This class defines the run_tests() entry point, plus a selection of other methods that are used to by run_tests() to set up, execute and tear down the test suite.</blockquote>
I also updated the <strong>create_test_db()</strong> functions with the new <strong>setup_databases() </strong>and <strong>teardown_databases()</strong> methods.
<h3>How you can use it</h3>
Here is my fork of danielfm's unittest-xml-reporting project with the updated multiple database support.

<a href="https://github.com/daspecster/unittest-xml-reporting">https://github.com/daspecster/unittest-xml-reporting</a>

You can clone this project...
<blockquote>git clone git@github.com:daspecster/unittest-xml-reporting.git</blockquote>
Or download it from the url above. Just make sure that you get the <strong>master</strong> branch.

To start using this code in your project you will need to install this code and then include the django TEST_RUNNER information in your settings.py.
<ol>
	<li>After you've gotten the code from git, you'll need to go into the unittest-xml-reporting directory and run $ <em>python setup.py install</em>,  as <strong>root.</strong> This will install the project into your python path.</li>
	<li>Now you need to tell django that you want to use this. You'll need to add these lines to your django project's settings.py file
<code>TEST_RUNNER = 'xmlrunner.extra.djangotestrunner.XMLTestRunner'
TEST_OUTPUT_VERBOSE = True
TEST_OUTPUT_DESCRIPTIONS = True
TEST_OUTPUT_DIR = 'xmlrunner'</code></li>
	<li>Now you should be able to run $ <em>python manage.py test </em>and it will create a folder called <em>xmlrunner</em> that has all your XML for the results of your tests!</li>
</ol>
