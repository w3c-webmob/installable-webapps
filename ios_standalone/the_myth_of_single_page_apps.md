# The state of standalone apps on iOS
For this study, we examined 360 web applications that claim to be capable of running "standalone" in iOS (i.e., the web application asserts that it's usable outside the context of iOS's default browser). We put those claims to the test by manually checking if the apps could, in fact, be used by user as standalone. To make sure our study is as representative as possible, we randomly selected the apps we tested from Alexa's top 78,000 websites. 

## Add to home screen
Through the use of the "add to home screen" option in Safari, iOS has allowed users to add web apps to the home screen of an iPhone since the release of iOS2.1 back in 2009. Web developers could make use of this capability to put their web apps on an equal footing as native apps on the user's home screen.

<figure>
![](images/github.png)
<figcaption>The "Add to home" feature on the iPhone.</figcaption>
</figure>

Over the last 4 years, this capability has seem some uptake in the wild, with iPhone users occasionally encountering a custom pop-up banner that request that they "install" the website they are viewing to the home screen.

<figure>
![](images/add_to_homescreen.jpg)
<figcaption>It's not uncommon to find web applications that ask the user to "install this web app on your iPhone: tap <icon> and then **add to homescreen**" on the iPhone.</figcaption>
</figure>

There are some obvious issues with this pop-up banner approach: not only is it inconsistent across web applications, but it requires developers to both "sniff" for the browser, and then tie a <abbr title="user interface">UI</abbr> component of their own website to that of Safari. 

This is a gamble on the part of the developer, in that Safari can change the look and position of this button at anytime. This problem can be clearly seen above: note there are two kinds of buttons (shown in detail below). If Apple was to relocate or change the look of this button (as it did in iOS7!), it could potentially lead to confusion amongst users.

<figure>
![](images/bookmark.png)
<figcaption>On the left, the iOS6 bookmark button. On the right, the iOS7 bookmark button.
</figcaption>
</figure>

It also means that if another browser tries to provide this functionality, it will have to put the bookmark button in the same location as Safari. Or the burden is put on developers to create a new popup banner that points to the right spot in the new browser, so users will then know how to add the web application to the home screen. 

Chrome Beta for Android is [experimenting with this capability](https://developers.google.com/chrome/mobile/docs/installtohomescreen), so the above may actually start occurring sooner rather than later.   

## Purpose of this study
The ability to install a web application to the home screen of a device is currently a hot topic at the W3C (see [manifest spec](http://w3c.github.io/manifest/)). As there is no standardized way to do this in browsers, there are a number of working groups trying to piece together all the bits that would be needed to make  installable web apps a standard part of the web platform.    

We hope this study can help inform the standardization of installable web apps currently taking place at the W3C. In particular, we hope that by looking at how developers are making use of the dominant proprietary mobile platform that provides this "add to home screen" capability, we can get an insight into the challenges users, developers, and implementers will face if akin technologies are standardized through the W3C and then become a part of the Web platform. 

## Definitions 
A web application <dfn>claims to be standalone</dfn> if it declares the following in its markup:

```
<meta name="apple-mobile-web-app-capable" content="yes">
```

Or its XHTML equivalent:

```
<meta name="apple-mobile-web-app-capable" content="yes" />
```

<dfn>Navigated</dfn> means that the user can follow hyperlinks (or interact with the document) without being thrown back into the default web browser. 

## Key questions
This study set out to answer the following questions. From the sites that claim to function as standalone:

 * What percentage of web apps are truly able to function as standalone? 
 * How many sites have a custom icon? 
 * What percentage of web apps claim to be standalone, but are actually just desktop sites? 
 * What percentage of web apps are standalone and mobile, but don't declare an icon?
 * How many sites claim to be standalone, but have a mistake in their markup that prevents them from working as standalone?

## Key findings
The number of sites claiming to run as standalone is small but significant. Of the 78,155 sites we used as data, they represent 1.4% of the dataset (i.e., 1097 claim to be "`apple-mobile-web-app-capable`").

```
1097/78,155 = 1.4%  
```

Despite their claims to the contrary, what we found was that the majority of web apps **do not** run as standalone (90% or 324 out of 360). Only a tiny fraction (10%, or 36 out of 360) are able to run as standalone - and 28% of those had significant limitations. There are, in fact, greater percentage (12%) of desktop sites masquerading as installable web apps than there are actual standalone applications. 

Of those 36 apps that were true standalone web apps, 10 (28%) of those had issues where they either left the user stranded without being able to "go back" - or worst, suddenly navigated to the desktop version of the site. In other cases, the application mostly worked - but then it was not possible to perform critical task (e.g., a purchase) in the application. In such cases, the application returned the user back into Safari.

Of the sites that did meet our criteria for a true standalone application (has an icon, is usable on mobile, can be navigated), many were quite limited leaving users stranded on random web pages without the ability to "go back". Others, like nest.com, make a best effort at working at standalone, but throw the user back to the default web browser at either random points - or for critical tasks, such as making a purchase.  

On the up-side, the majority of sites (76%) where designed to work on a mobile phone, even if only (13%) of those could actually be navigated.

Icon usage, overall, was also fairly healthy - 56% of the sites we tested included an icon. However, we discovered that at least some sites included dummy icons from purchases templates - meaning more than one site included an icon that had nothing to do with the site itself.

Oddly, many sites (5% or 19) incorrectly claim that they can run as standalone -  but contain a markup error in their HTML that prevents the application from actually doing so! Ironically, of those, 12 out of 19 (63%) even go as far as to include an icon. 

For more details, see the the "other observatons" section, as well as the "all the questions" section.

## Criteria 
The following is the criteria that we assert an application must meet in order to be a <dfn>true standalone application</dfn>. 

Firstly, the web application must have an icon that allows it to be distinguished amongst native applications. This is illustrated below, where the Slashdot icon is easy to locate amongst native iOS applications. 

<figure>
![](images/slashdot_icon.png)
<figcaption>Slashdot icon amongst native apps.</figcaption>
</figure>
 
Secondly, all critical functionality of the application is self contained, without requiring browser chrome to make the application usable. Again, the Slashdot web application running as standalone serves to exemplify such functionality. 

<figure>
<video src="video/slashdot.mp4"> 
<figcaption>Slashdot is fully functional as an application. When necessary, it provides its own interface elements to enable navigations (e.g., a back button).</figcaption>
</figure>

Thirdly, the web application must be usable on a mobile phone. That is, the application's creator has made an effort to adapt the content of the application to a mobile device — particularly an iPhone. The criteria we used here was: either the app's creator has made an obvious effort to use common conventions found on mobile web applications (e.g., a menu button at the top right hand side of the screen, as shown below); or the content of the web application is legible and UI components are usable without requiring the user to zoom in (achieved by explicitly declaring a `<meta name="viewport" content="width=device-width">`). 

<figure>
![](images/mobile_vs_desktop.jpg)
<figcaption>Nest, on the left, exemplifies a typical "mobile site". The Squawka site on the right exemplifies a desktop site masquerading as a standalone web application. Note how the Squawka site would not be easy to use on a mobile device (requires the user to zoom in, pan around, etc.)</figcaption>
</figure>

## Methods and limitations
This study was conducted using the [webdevddata.org](http://webdevddata.org) dataset. The data was collected over an  approx. 8-12 hour period on the 31st of October, 2013. Over those hours, the response page from 78,155 domains were collected (the crawler follows redirects and saves any `HTTP 200 OK` response). The [source for the crawler](https://github.com/Webdevdata/fetcher) is available on GitHub.  

The domains are fetched in order (from most popular to least) from Alexia's top 1 million sites at the time the data was downloaded. Note that some domains return the same data (e.g., google.com, google.co.uk, etc.). It is assumed that the size of the dataset reduces the influence of these duplicate domains.   

The dataset was filtered for files that matched the CSS selector `meta[name="apple-mobile-web-app-capable"][content="yes"]` (i.e., any `meta` that has a name attribute "`apple-mobile-web-app-capable`" and whose `content` attribute is "`yes`"). This search was done using a custom tool, which was developed by the WebDevData Community Group. The tool makes use of a HTML parser, so to avoid false positives that would result from simply doing a text search. The tool does not load or execute scripts, however. This means that any website that dynamically inserts `meta` elements cannot be matched by the tool. We assumed that relatively few, if any, sites actually do this - primarily because of the frequency in which `meta` elements appear in HTML pages.  

The list of the resulting 1097 matching files are available as a [gist on Github](https://gist.github.com/ernesto-jimenez/9073492). Statistically speaking, we consider this our [population](http://en.wikipedia.org/wiki/Statistical_population) - i.e., our "set of individuals or objects of interest" as defined on Wikipedia.

To define our sample size, we applied [Cochran]'s correction formula for populations sizes less than 50,000: 

```
n1 = 384/(1+384/1097)= 284
```

So, according to [Cochran]'s correction formula, a minimum of 284 sites would need to be sampled to attain a 95% [confidence level](http://www.stats.gla.ac.uk/steps/glossary/confidence_intervals.html#conflevel) (error of 5%). Because we knew there would likely be issues with the sites (e.g., site is down, etc.), and because of redundancies (discussed below), we followed an oversampling technique and randomly selected 500 sites instead. From the 1097 sites, in order to then derive the random sample, the following ECMAScript was used over the data set.  

```
rand = []; 
for(var i = 0; i < 500; i++){ 
  var randKey = Math.random() * data.length; 
  var itemKey = Math.floor(randKey);
  //add it to our collection 
  rand.push(x[itemKey]);
  //remove item just collected 
  x.splice(itemKey, 1);
}
rand.join(",\n")
```

Although we had 500 sites to sample, the reason we ended up with 360 sites was because of time constraints and the redundancies described below. Each site takes about 1 minute to load and check. The sites where manually loaded in Apple's iOS Simulator over a 4 day period between 16-20th of February. The settings for the simulator were "iPhone Retina (4-inch 64Bit)" simulating iOS 7.0. This is shown below.  

<figure>
![](images/simulator.png)
<figcaption>iOS simulator and settings</figcaption>
</figure>

The data collected is available as a CVS file on GitHub.

The data is split across four columns:

<dfn>
<dt>site</dt> 
<dd>The domian of the site being examined.</dd> 
<dt>icon</dt>
<dd>If the application includes a custom icon</dd>
<dt>mobile</dt>
<dd>Is the site a mobile site.</dd>
<dt>navigates</dt>
<dd>Once launched, is it possible to navigate around the application?</dd>
</dfn>

The data is coded as follows:

<dl>
 <dt>0</dt><dd>"no"</dd>
 <dt>1</dt><dd>"yes"</dd>
 <dt>-1</dt><dd>"markup error". Only applies to the "navigation" column.</dd>
</dl>
 
The data was then inported into [SQLite3](http://www.sqlite.org/). 

```
.mode csv
.import apps.csv webapps
```	

As all we needed was count and percentages, SQL queries were then used to perform the statistics. See the All Questions section for the actual SQL used.  

### Redundancies and issues in the data
Although all the domains in the data set are unique, some domains return the same data as other domains. For example:

* [sc.com](http://sc.com) is the same as [standardchartered.com.sg](http://standardchartered.com.sg)
* Others redundant sites included, pricegrabber.co.uk, katproxy.com, pscufs.com, rezultati.com, suite101.net, and meusresultados.com. 

Some sites returned a `HTTP 403 Forbidden` or simply would refused to connect. This happened even though they worked fine when the original dataset was collected in October 2013: 

* [trknck.com](http://trknck.com)
* [partnerspay.com](http://partnerspay.com)
* [pixable.com](http://pixable.com)

Some sites did not provide enough information to test all three aspects (icons, navigation, mobile). For example, [webcamtoy.com](http://webcamtoy.com) contains an icon, is mobile, but doesn't provide any interaction or navigation: it tells the user to go to the desktop site instead. As such, it was excluded. 

<figure>
![](images/webcamtoy.png)
<figcaption>[webcamtoy.com](http://webcamtoy.com) tells the user to load the desktop site instead.</figcaption>
</figure>

Some sites declared themselves as standalone through markup, but when loaded in Safari redirect to a mobile version that excludes the required markup. Some examples of sites that do this:

 * [soniarykiel.com](http://soniarykiel.com)
 * [tapiture.com](http://tapiture.com)
 * [pullandbear.com](http://pullandbear.com)
 * [www.larena.it](http://www.larena.it)

## Other observations
This sections notes some observations that were made during data collection. Some are quite amusing :)

Some sites, like [youbeli.com](http://www.youbeli.com/), ask the user to add their application to the home screen. However, after the user relaunches the application and clicks on any links, they are thrown back into the browser. 

A big challenge with installable web apps is having to change large amounts of backend infrastructure to support them. E.g., forums, payment, etc. 

# All questions
This section listes the questions that we could ask from the data we have, as we as how those questions are express as SQL. 

### What percentage of web apps are truly able to function as standalone?

**Answer**: 10%. See the definition of a truly standalone application. See also the caveats below. 

```
select count(*) from webapps where icons is "1" and navigates is "1" and mobile is "1";
36
```

Some applications allow navigation, but then unexpectedly navigate to the desktop version of the site:

* radardedescontos.com.br
* soluto.com
* kingcounty.gov 

Some sites provide simple interactions like searching. However, they throw the user back into the browser for any critical functionality (e.g., making a purchase):

* nest.com
* songkick.com
* suite101.fr 
* urbita.com

The following sites work initially, but then leave the user stuck at certain pages. As there is no back button, there is not much the user can do but to quit the app:

* sumall.com
* wisedock.de 
* comediansincarsgettingcoffee.com 


### What percentage of web apps claim to be standalone, but are actually just desktop sites? 
**Answer**:

```
select count(*) from webapps where icons is "0" and navigates is "0" and mobile is "0";
43
```
12%

### How many sites are mobile?
**Answer**:
```
select count(*) from webapps where mobile is "1";
274
``` 
76%

### How many sites are desktop sites?
**Answer**:
```
select count(*) from webapps where mobile is "0";
86
```
24%

### How many sites have a custom icon? 
**Answer**:56%.

```
select count(*) from webapps where icons is "1";
202
```

Even though some sites have an icon, the icon is actually from a purchased theme (my theme shop) so  Hence doesn't match the application. Further evidence that developers don't check their sites or templating will cause issues in the future for installable web apps. 

 * pixelbell.com
 * smashfreakz.com

### How many sites DO NOT have a custom icon?
**Answer**: 44%. 

```
select count(*) from webapps where icons is "0";
158
```

### How many sites can be navigated (irrespective of having an icon or being a mobile site)?
**Answer**: 15%.

```SQL
select count(*) from webapps where navigates is "1";
53
```

### How many sites are desktop sites that can be navigated?
**Answer**: 2%.

```SQL
select count(*) from webapps where navigates is "1" and mobile is "0";
6
```


### How many sites are desktop sites that can be navigated and have an icon?
**Answer**: 1%.

```SQL
select count(*) from webapps where navigates is "1" and mobile is "0" and icons is "1";
2
```


### How many sites are desktop sites, but include an icon?
**Answer**: 11%.

```SQL
select count(*) from webapps where icons is "1" and mobile is "0";
38
```



### How many sites can be navigated, are mobile, but don't declare an icon?
**Answer**: 3%.

```SQL
select count(*) from webapps where icons is "0" and navigates is "1" and mobile is "1";
11
```


### How many sites claim to be standalone, but have a mistake in their markup that prevents them from working as standalone?
**Answer**: 5%.

```SQL
select count(*) from webapps where navigates is "-1";
19
```

### How many sites that don't work as standalone inlcude an icon?

```SQL
select count(*) from webapps where navigates is "-1" and icons is '1';
12
```

# References
<dl>
<dfn>[Cochran]</dfn> 
<dd>Cochran, W. G. (1977). Sampling techniques (3rd ed.). New York: John Wiley & Sons.</dd>
<dt>[Apple]</dt>
<dd>[Supported Meta Tags]()</dd>
</dl>