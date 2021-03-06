Googael Analytics v0.4
======================
####*IP based geolocation for Apache access log*

 Copyright (C) 2013 Gael Abadin<br/>
 License: [MIT Expat][1]<br />
 [![Code Climate](https://codeclimate.com/github/elcodedocle/geogoogael.png)](https://codeclimate.com/github/elcodedocle/geogoogael)

## What this is

A marvelous piece of software you can roll on your apache web server in order to get some geographical info about your site's visitors on a super cool map, chart and table.  Check it all out working in this [demo][2].

![Geogoogael test site snapshot with data from bundled fake access_log generator](http://i.imgur.com/1XTHzX9.png "This is how geogoogael's test site looks like. Data is fake on this site! (generated by geoogogael's fake access_log generator. Check it out!)")

## What this is not

A serious web traffic analytics or maps rendering tool.

If you know all about KPIs, mapnik, geoJSON, PostGIS geometries, etc. you are probably wasting your time here: This is just an amusement, not precisely a proper web analytics tool with an embedded GIS, but if you find it useful and miss any features I'm open to suggestions.

So, that's it.

## Change Log

### UPDATE v0.4 

* Client-side input validation. 
* REST-alike clean URLs. 
* Masked IPs option. 
* Optimized access log parsing. 
* HTTPBasicAuth support. 
* A lot of refactoring.

### UPDATE v0.3 

* Optimized database queries.
* Error message handling.
* Fake `access_log` file generator (for testing purposes and show off).

(I wanted to see how this app would perform on huge access_log files, but didn't have any, so I ended up overkilling the issue by designing the nastiest, most awesome `access_log` generator the world will ever ignore, using discrete event statistical modeling theory, forked processes and shared memory with signaling and semaphores and all kinds of freaky stuff. Check its [code](https://github.com/elcodedocle/geogoogael/blob/master/geogoogael/test/apache_fake_access_log_generator.php) for more info ;-))

### UPDATE v0.2 

* Super cool zoomable timeline chart with granularity modulation (visits per minute, hour, day or month).

## Known Bugs

I have not the time or the patience to test this code thoroughly so, as Doctor Knuth would say, "I have only proven it correct". Since my skills are nowhere near Doctor Knuth's, beware of the many bugs and help me clean the code by [reporting them][2] (I'll fix anything reported ASAP.) 

## How to install/config/deploy

* Read comments at the beginning of [setup.php](https://github.com/elcodedocle/geogoogael/blob/master/geogoogael/setup/setup.php) file.

## How to use

* After deployment, hit deployment location.

## TODO

* Filters on the map markers and chart data points. 
* Gettext translations. 
* Support for different access_log formats. 
* .htaccess tweaks. 
* Websockets based real time option (v0.5).
* Snippety thingy for selective logging (v0.6).
* Wordpress/Drupal plugin. 
* Android client.

 
## Acknowledgments

Everybody behind this thick fraking stack that makes the awesome possible.

## Want to contribute?

1. [Fork me][3] on github 
2. `git checkout -b newbranch` and `git push origin newbranch` your commits
3. Make a [pull request](https://github.com/elcodedocle/geogoogael/compare/) from your branch

AND/OR

* Buy me a beer! ( [Paypal][4] or [Bitcoin][5]: 15QjBzCVckAwtLK5v95M8GS2tbpnTwKm5B )

## FAQ

**Q**: I can't access the app on the specified location when setup finishes.<br/>
**A**: You probably have a conflict with an existing .htaccess on your server. Add these two lines at the top of all your previously existent .htaccess files on the path to the one generated by setup.php, right after `RewriteEngine on` line:
```apache
RewriteCond %{REQUEST_URI} ^/uri/path/to/geogoogael/parent/folder(/.*)?$
RewriteRule (.*) $1 [L]
```
(of course you need to replace the path with the real path to the app's deployment folder from the webroot)

**Q**: Does it work on windows?<br/>
**A**: No. You should be able to patch it and have it working in about 5 minutes, though. This is because I don't like or care about WAMP very much. (Sorry)

**Q**: It is working, but why so darn slow?<br/> 
**A**: Maybe you are not caching database queries? Try enabling cache on you my.cnf mysql/mariadb server config file and setting cache size to at least 16MB. On big log files some requests can still take more than a minute at first, probably due to the log file not being cached on the RAM yet.

**Q**: Why did you go all this way instead of just using google analytics?<br/>
**A**: There may be a better explanation in the foreseeable future, but mainly because I could do it and felt like doing it.

**Q**: To be clear... Is there any advantage on using this over google analytics?<br/>
**A**: None that I can think of... Nope. None at all.

**Q**: Can I use this code commercially?<br/>
**A**: Yes, you can. 

Specifically, this code and the libraries it uses (which you will find on geogoogael/lib folder) have GPLv2 compatible licenses that allow commercial use free of charge, with two notable exceptions: [Google Maps API][6] and [highcharts plugin][7], both with available licensing options for commercial use which are not free of charge (check out the links for pricing). About the geolocation database, it is available for free for commercial use, as long as the terms stated [here][8] are met. 

This product includes IP2Location LITE data available from [http://www.ip2location.com][9]

There you go. Have fun.


[1]: https://github.com/elcodedocle/geogoogael/blob/master/LICENSE
[2]: http://tester:retset@geovolutions.com/geogoogael/test
[3]: https://github.com/elcodedocle/geogoogael/fork
[4]: http://goo.gl/zCDmg5
[5]: bitcoin:15QjBzCVckAwtLK5v95M8GS2tbpnTwKm5B
[6]: http://goo.gl/XC8UjG
[7]: http://goo.gl/dq0bwj
[8]: http://lite.ip2location.com/terms-of-use
[9]: http://www.ip2location.com
