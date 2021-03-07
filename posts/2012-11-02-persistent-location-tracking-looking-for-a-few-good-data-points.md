---
title: "Persistent Location Tracking: Looking For A Few Good Data Points"
date: 2012-11-02
tags:
  - Location
  - Technical
layout: layouts/post.njk
---

In this post, I revisit the question of whether Google Latitude meets my persistent location tracking needs. In [my previous post](/posts/2012-10-29-persistent-location-tracking-picking-the-right-tool/), I compared Google Latitude to InstaMapper and concluded that the latter is too battery-intensive. By looking at maps and base-level insights from the data, I suggest that Google Latitude optimizes for battery life at the expense of data quality.

<!-- more -->

## Exhibit A: Some Maps

I started gathering data on Oct. 3, 2012:

<img src="https://lh5.googleusercontent.com/-kyl-kUDWe_M/UJgVi3pls3I/AAAAAAAAALg/zGsaBfNzY7s/s640/map-monthly.jpg" />

Since then, [Valkyrie Savage](http://www.eecs.berkeley.edu/~valkyrie/) and I have travelled to Boston and Chicago. Our stopover in Phoenix is clearly visible at this scale. You can barely make out our day trip to [Mount Monadnock, NH](http://goo.gl/maps/rLfNu) over near Boston. Here's a closer look at that trip:

<img src="https://lh4.googleusercontent.com/-YJQip0zWnxQ/UJgVlFc_7pI/AAAAAAAAAMA/DjlCRjxouzo/s640/map-monadnock-trip.jpg" />

Ouch. The data is *noisy in some areas, sparse in others.* It's fairly clear that we took Hwy 2 over, but *some of the GPS readings are miles off.* Let's zoom in on that hike:

<img src="https://lh5.googleusercontent.com/-bg3DxaZTe6k/UJgVlqpW7ZI/AAAAAAAAAMI/t2Kn3hrhWJM/s640/map-monadnock-hike.jpg" />

Only five data points actually lie within the park/mountain boundaries. That's *five data points for a four-hour hike.* Our Boston data is somewhat more accurate:

<img src="https://lh3.googleusercontent.com/-6RFwbwjBEtI/UJgVmQk1KCI/AAAAAAAAAMQ/-Nhyp0LtoLw/s640/map-monadnock-boston.jpg" />

Still, the red line cuts through city blocks with reckless abandon. Either we're flying, or we're packing some incredibly efficient demolition equipment.

Here's the map for one of my more itinerant Bay Area days:

<img src="https://lh5.googleusercontent.com/-xNNR5dnNV44/UJgVj3SZAEI/AAAAAAAAALw/6KvtDZYWel0/s640/map-busy-day.jpg" />

I cycled to a doctor's appointment, visited [BiD](http://bid.berkeley.edu/) to hear [Mary Czerwinski](http://research.microsoft.com/en-us/people/marycz/) speak about emotion tracking, worked from [home](http://goo.gl/maps/z7EuA) for a bit, went into San Francisco to meet up with [Lev Popov](http://www.linkedin.com/in/levpopov), and finally dragged myself home again.

The BART ride into San Francisco is understandably sparse: most of it is separated from cell towers and GPS satellites by rock and/or water.

Most of my travel is on foot, by bike, or via public transit. Not content with the Mount Monadnock hike data, I tried another quick drive up into [Tilden](http://goo.gl/maps/zk3AD):

<img src="https://lh5.googleusercontent.com/-MCZ55KYjgcE/UJgVjNWQ0FI/AAAAAAAAALo/pibM6xiJmUE/s640/map-drive-test.jpg" />

Google Latitude captured *just four points during the 20-minute drive.*

## Exhibit B: Some Analysis

You can see the code for this analysis [here](https://github.com/candu/quantified-savagery-files/tree/master/Location/kml) and [here](https://github.com/candu/quantified-savagery-files/tree/master/Location/api).

After trudging through several lackluster map views, I'm left with a nagging impression:

{% blockquote %}
This data isn't that useful.
{% endblockquote %}

This impression deserves further analysis, so I grab the KML to answer some of my questions. First off: *how often is Google Latitude checking my location?*

<img src="https://lh5.googleusercontent.com/-A7we5G7pYIw/UJb-xhCk_oI/AAAAAAAAAKk/O7ZwpxF_uQs/s640/timings-frequency.jpg" />

*About every two minutes.* GPS is a [huge battery drain](/posts/2012-10-29-persistent-location-tracking-picking-the-right-tool/); increasing the time between updates can help by allowing the GPS radio to enter an idle state. *How are those location readings scheduled?*

<img src="https://lh6.googleusercontent.com/-PMYu61X440I/UJb-yCEbuBI/AAAAAAAAAKs/umbJNuuVfo0/s640/timings-second-histogram.jpg" />

Google Latitude really likes spacing its readings out by a *whole number of minutes.*

*How accurate is the data?* The KML doesn't provide [accuracy estimates](http://en.wikipedia.org/wiki/Dilution_of_precision_(GPS)) for its locations. Fortunately, the [Google Latitude API](https://developers.google.com/latitude/) does, so I retrieve my data using [this script](https://github.com/candu/quantified-savagery-files/blob/master/Location/api/scrape.py) and look at the accuracy readings:

<img src="https://lh3.googleusercontent.com/-p5senVUtgqM/UJb-ybk3zEI/AAAAAAAAAK0/qUvLSvog15E/s640/accuracy-histogram.jpg" />

Actually, *the readings have fairly high accuracy.* Only 7% of readings have a reported error radius greater than 100m.

The maps above suggest that location readings are less accurate while travelling at high speed. Is that true? The API provides speed estimates for some readings, but this data is kind of sparse:

```
$ python speed.py < history.api
found 7429 speed values among 20898 readings
```

I try a different method: the [Haversine distance formula](http://mathforum.org/library/drmath/view/51879.html), which gives me the distance between two points on the Earth's surface:

```py
def haversineDistance(A, B):
  """
  Distance (in meters) between two Locations. Uses the Haversine formula.

  See http://www.movable-type.co.uk/scripts/latlong.html for corresponding
  JavaScript implementation.
  """
  # Earth's radius in meters
  R = 6371009
  dLat = math.radians(B.lat - A.lat)
  dLon = math.radians(B.lng - A.lng)
  lat1 = math.radians(A.lat)
  lat2 = math.radians(B.lat)
  sLat = math.sin(dLat / 2.0)
  sLon = math.sin(dLon / 2.0)
  a = sLat * sLat + sLon * sLon * math.cos(lat1) * math.cos(lat2)
  c = 2.0 * math.atan2(math.sqrt(a), math.sqrt(1.0 - a))
  return R * c
```

I use this distance formula to get a plot of accuracy versus travelling speed:

<img src="https://lh5.googleusercontent.com/-ba4lES16aCU/UJb-ytwI4OI/AAAAAAAAAK8/-OZvTHzgZjk/s640/accuracy-vs-speed.jpg" />

*No clear correlation here*; there are low-quality readings at both low and high speeds. There are several possible explanations:

- **Confirmation bias:** I mistakenly extrapolated a small handful of low-quality readings taken at high speeds to a general pattern.
- **Misinterpretation:** Some of the Mount Monadnock readings look way off; perhaps the error radius doesn't mean what I think it does.
- **Different location sources:** Location accuracy is [relatively well-defined](http://en.wikipedia.org/wiki/Dilution_of_precision_(GPS)) for GPS, but I'm not sure what happens when cell towers or WiFi access points are incorporated into location fixes.
- **Longer sampling interval:** Maybe Google Latitude assumes that precise location tracking is less important when driving.

To test this last hypothesis, I also *plot sampling interval versus speed:*

<img src="https://lh5.googleusercontent.com/-__3m3z_oQfQ/UJcC4GeNhyI/AAAAAAAAALQ/HI6XQdHjtns/s640/timings-vs-speed.jpg" />

Nothing conclusive there.

## Conclusion

*The problem appears to be sampling frequency.* To reduce battery usage, *Google Latitude polls about once every two minutes.* While it has some mechanism for polling more often in periods of high activity, it's unclear how that works.

Reliance on fixes from cell towers and WiFi may be reducing location quality in more remote areas. Testing this hypothesis is difficult: how do you quantify remote? One possibility is to compute nearest-neighbor distance against [a database of cities](http://www.maxmind.com/en/worldcities). Another confounding factor is the reliability of those `accuracy` values. Improving upon that would likely involve manual labelling.

## Why Do This?

{% blockquote %}
Accuracy is not binary.
{% endblockquote %}

In Quantified Self applications, we *use personal data to drive changes in our lives.* We put a lot of trust in the accuracy and relevance of that data, and *we extend that trust to the tools and services that collect it.* We trust [Fitbit](http://www.fitbit.com/) to track our fitness. We trust [Zeo](http://www.myzeo.com/sleep/) to improve our sleep. We trust [Lumosity](http://www.lumosity.com/) to train our perception and attentiveness.

In giving so much trust to these tools, we sometimes forget that *data are not infallible.* [Physics guarantees](http://www.pbs.org/wgbh/aso/databank/entries/dp27un.html) that there is no such thing as perfect data. *All data contain error.* As a system consisting of geosynchronous satellites that travel at relativistically significant speeds and beam data through our multilayered atmosphere to tiny chip radios sandwiched between layers of dense circuitry, GPS is understandably [error-prone.](http://www.kowoma.de/en/gps/errors.htm) When your chosen tools and services add noise on top of that, it's reasonable to ask:

{% blockquote %}
How much trust should I place in the output?
{% endblockquote %}
