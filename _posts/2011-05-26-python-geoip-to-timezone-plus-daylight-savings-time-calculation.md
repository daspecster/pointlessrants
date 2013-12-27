---
layout: post
title: 'Python GeoIP to TimeZone! Plus Daylight Savings Time calculation!'
tags:
  - datetime
  - daylight-savings-time
  - dst
  - geoip
  - maxmind
  - python
  - pytz
  - timezone

---

Some of you may have <a title="Python-GeoIP Python" href="http://www.pointlessrants.com/2010/05/python-geoip-python-geoip-cities-tutorial/">read my article about python-geoip for mapping an IP to a city.</a>

If you provide a service which relies on timezones or even just want to display a message at that time then being able to map an IP address to a timezone can be valuable.

This assumes that you have the GeoLiteCity.dat database and that it's all setup and working. I can show you how to do that in <a title="Python-GeoIP City" href="http://www.pointlessrants.com/2010/05/python-geoip-python-geoip-cities-tutorial/">this article</a>.

Once you have that all setup and working all you have to do to get the timezone is pass the country code and region to the GeoIP library function GeoIP.time_zone_by_country_and_region() function.

Here's an example...

<code>&gt;&gt;&gt; import GeoIP
&gt;&gt;&gt; GeoIP.time_zone_by_country_and_region(gi.record_by_addr("74.125.93.106")['country_code'], gi.record_by_addr("74.125.93.106")['region'])
'America/Los_Angeles'
</code>
<h3>PyTZ</h3>
<a title="PyTZ Python TimeZone Library" href="http://pytz.sourceforge.net/">PyTZ</a> is a nice library that you can use to manipulate timezones in python.

If you want to find out the timezone for an IP address you'll need to pass it through PyTZ.

<code> &gt;&gt;&gt; from pytz import timezone
&gt;&gt;&gt; tz = timezone(GeoIP.time_zone_by_country_and_region(gi.record_by_addr("74.125.93.106")['country_code'], gi.record_by_addr("74.125.93.106")['region']))</code>
<h3>Calculating Daylight Savings Time (DST)</h3>
<code> &gt;&gt;&gt; from datetime import datetime
&gt;&gt;&gt; loc_dt = tz.localize(datetime(2011,5,26,16,0,0))
&gt;&gt;&gt; loc_dt.dst()
datetime.timedelta(0, 3600)
&gt;&gt;&gt; loc_dt = tz.localize(datetime(2011,12,26,16,0,0))
&gt;&gt;&gt; loc_dt.dst()
datetime.timedelta(0)
</code>

Here you can see that on May 26th 2011 the DST 3600 seconds (an hour), then on December 26th 2011 the DST is 0.
<h3>Summary</h3>
So here's the complete code for figuring out daylight savings time from an IP...

<code> &gt;&gt;&gt; import GeoIP
&gt;&gt;&gt; from pytz import timezone
&gt;&gt;&gt; from datetime import datetime</code>

<code> </code>

<code>&gt;&gt;&gt; gi = GeoIP.open("/usr/share/GeoIP/GeoIPCity.dat", GeoIP.GEOIP_STANDARD)
&gt;&gt;&gt; googles_tz = GeoIP.time_zone_by_country_and_region(gi.record_by_addr("74.125.93.106")['country_code'], gi.record_by_addr("74.125.93.106")['region'])
&gt;&gt;&gt; tz = timezone(googles_tz)
&gt;&gt;&gt; loc_dt = tz.localize(datetime(2011,5,26,16,0,0))
&gt;&gt;&gt; loc_dt.dst()
datetime.timedelta(0, 3600)
&gt;&gt;&gt; loc_dt = tz.localize(datetime(2011,12,26,16,0,0))
&gt;&gt;&gt; loc_dt.dst()
datetime.timedelta(0)
</code>
