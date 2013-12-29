---
layout: post
title: 'Python GeoIP (python-geoip) cities tutorial '
tags:
  - firefox
  - geo-ip
  - geolocation
  - maxmind
  - python
  - twitter

---

Using <a title="Wikipedia Geolocation" href="http://en.wikipedia.org/wiki/Geolocation">geolocation</a> is something that people are doing a lot lately.  You may have noticed twitter.com in FireFox showing a little bar at the top asking if it's alright to share your location. This is so that when you tweet you can have your location show up there. That way you can keep track of where you tweet from.  There are many uses for this kind of information and these days there's a lot of free things out there to help you get started with your geolocation project.
<h2>Installing GeoIP</h2>
Requirements/Dependancies:
<ul>
	<li>Python 2.4+</li>
	<li>python-geoip</li>
	<li>libc6</li>
	<li>libgeoip1</li>
</ul>
More on dependencies here <a title="Ubuntu Karmic GeoIP python-geoip" href="http://ns2.canonical.com/es/karmic/python-geoip">http://ns2.canonical.com/es/karmic/python-geoip</a>. <em>But don't worry about these since most of them get installed by the package anyway.</em>

A couple of basic principles before we get started.
<ol>
	<li>Geolocation is gathered from an IP address.</li>
	<li>There has to be a database that connects the IP address to a geographical location</li>
</ol>
I'm going to be using Python here because frankly it's powerful, easy and has awesome libraries for geolocation. Which brings me to the <a title="Ubuntu Karmic GeoIP python-geoip" href="http://ns2.canonical.com/es/karmic/python-geoip">GeoIP</a> library! I'm using Ubuntu 9.10 so most of these libraries will just take an apt-get to install.

Then you can install python-geoip with
<pre>sudo apt-get install python-geoip</pre>
Or you can get the source from <a title="MaxMind GeoIP python" href="http://geolite.maxmind.com/download/geoip/api/python/">http://geolite.maxmind.com/download/geoip/api/python/</a>

Now that you have this installed you can  test it with the following code put in the python terminal.

```python
import GeoIP
gi = GeoIP.new(GeoIP.GEOIP_MEMORY_CACHE)
print gi.country_code_by_addr("203.195.93.0")
```

I got that from MaxMind's tutorial <a title="MaxMind GeoIP tutorial" href="http://www.maxmind.com/app/python"><em>http://www.maxmind.com/app/python.</em></a><em> </em>At this point you have the ability to track IPs down to the country level. What you probably really want is to go down to the city level.
<h2><span style="font-size: medium;">Geolocation - Cities</span></h2>
If you call some of the other functions on the GeoIP class like record_by_addr() you'lld get an error like this

<em>"Invalid database type GeoIP Country Edition, expected GeoIP City Edition, Rev 1"</em>

This is telling us that we don't have the database for the city level information. You can get that for FREE from MaxMind!

<a title="GeoIP City database MaxMind" href="http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz"><em>http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz</em></a>

There is a shell script available to update the city database for you in the python-geopip package (Don't forget to "chmod +x" on it!).

file: /usr/share/doc/libgeoip1/examples/geolitecityupdate.sh


```bash
#!/bin/shGUNZIP="/bin/gunzip"
MAXMINDURL="http://geolite.maxmind.com/download/geoip/database/"
WGET="/usr/bin/wget -q -O -"
TMPDIR=$(mktemp -d)
if [ ! -d "$DATADIR" ] ; then
echo "Data directory $DATADIR/ doesn't exist!"
exit 1
fi
if [ ! -w "$DATADIR" ] ; then
echo "Can't write to $DATADIR directory!"
exit 1
fi
cd "${TMPDIR}"
${WGET} "${MAXMINDURL}/GeoLiteCity.dat.gz" | ${GUNZIP} &gt; GeoIPCity.datif [ $? != 0 ] ; then
echo "Can't download a free GeoLite City database!"
exit 1
fi
mv -f "GeoIPCity.dat" "${DATADIR}/"
if [ $? != 0 ] ; then
echo "Can't move databases file to ${DATADIR}/"
exit 1
fi
exit 0
```

What this script does is..
<ol>
	<li>Download the database (<a title="GeoIP Databases" href="http://geolite.maxmind.com/download/geoip/database/">http://geolite.maxmind.com/download/geoip/database/</a>)</li>
	<li>unzips the file</li>
	<li>and moves it to /usr/share/GeoIP</li>
</ol>
Now this is the key! That database "GeoLieCity.dat" MUST be in that directory!

Then there is the magic piece of code that isn't really documented anywhere...

Except here in ubuntu, along with many other examples(hence the folder name "examples").


file: /usr/share/doc/python-geoip/examples

```python
gi = GeoIP.open("/usr/share/GeoIP/GeoIPCity.dat",GeoIP.GEOIP_STANDARD)
```
or...

```python
gi = GeoIP.open("/usr/share/GeoIP/GeoIPLiteCity.dat",GeoIP.GEOIP_STANDARD)
```
Depending on what you downloaded.

Creating a new instance of GeoIP with the path to the alternate database will give you access to all sorts of awesome information!
<h2>Ok, now all the code...</h2>
Find by IP address:

```python
gi = GeoIP.open("/usr/share/GeoIP/GeoIPCity.dat",GeoIP.GEOIP_STANDARD)
print gi.record_by_addr("74.125.95.105")
{
    'city': 'Mountain View',
    'region_name': 'California',
    'region': 'CA',
    'area_code': 650,
    'time_zone': 'America/Los_Angeles',
    'longitude': -122.05740356445312,
    'metro_code': 807,
    'country_code3': 'USA',
    'latitude': 37.419200897216797,
    'postal_code': '94043',
    'dma_code': 807,
    'country_code': 'US',
    'country_name': 'United States'
}
```
Find by name:

```python
gi = GeoIP.open("/usr/share/GeoIP/GeoIPCity.dat",GeoIP.GEOIP_STANDARD)
print gi.record_by_name("www.google.com")
{
    'city': 'Mountain View',
    'region_name': 'California',
    'region': 'CA',
    'area_code': 650,
    'time_zone': 'America/Los_Angeles',
    'longitude': -122.05740356445312,
    'metro_code': 807,
    'country_code3': 'USA',
    'latitude': 37.419200897216797,
    'postal_code': '94043',
    'dma_code': 807,
    'country_code': 'US',
    'country_name': 'United States'
}
```

Find PointlessRants!

```python
gi = GeoIP.open("/usr/share/GeoIP/GeoIPCity.dat",GeoIP.GEOIP_STANDARD)
print gi.record_by_name("www.pointlessrants.com")
{
    'city': 'Brea',
    'region_name': 'California',
    'region': 'CA',
    'area_code': 714,
    'time_zone': 'America/Los_Angeles',
    'longitude': -117.86119842529297,
    'metro_code': 803,
    'country_code3': 'USA',
    'latitude': 33.926898956298828,
    'postal_code': '92821',
    'dma_code': 803,
    'country_code': 'US',
    'country_name': 'United States'
}
```