---
title: PokeVision Load City
author: ETdoFresh
type: post
date: 2016-07-29T21:47:19+00:00
url: /pokevision-load-city/
categories:
  - Uncategorized

---
<img class="alignnone size-full wp-image-268" src="http://www.etdofresh.com/wp-content/uploads/2016/07/PokeVision.png" alt="PokeVision" width="893" height="572" /><!--more-->

Hey everyone. So I've been taking a peek at this [Pokevision][1] map and loving it! So, figured out the name of the function of what loads the pokemon nearby and decided I'll do the whole city of New Orleans using a simple For loop.

The javaScript function to find nearby pokemon was:

<pre lang="javascript" line="0">App.home.findNearbyPokemon(latitude, longitude)</pre>

So to load the entire city of New Orleans in about a minute... after loading PokeVision site, you have to open up a javascript console. In chrome, you click Menu > More Tools >  Developer Tools > Console. Paste the following into the javascript console.

UPDATE: Make sure the Java Console is up before loading the site

<pre lang="javascript">var radius = 0.01;
var latitude = 29.90;
var longitude = -90.28;
var minLatitude = 29.90;
var maxLatitude = 30.05;
var maxLongitude = -90.00;
var intervalBetweenFetches = 150;

function Fetch()
{
  console.log("Fetching " + latitude + ", " + longitude);
  App.home.findNearbyPokemon(latitude, longitude)
  latitude += radius;
  if (latitude &gt; maxLatitude)
  {
    latitude = minLatitude;
    longitude += radius;
  }
  if (longitude &lt;= maxLongitude)
    setTimeout(Fetch, intervalBetweenFetches);
}

Fetch();</pre>

Then you should be able to see where all those pesky pokemon are hiding.

 [1]: https://pokevision.com/#/@29.972873556540357,-90.12580633163451