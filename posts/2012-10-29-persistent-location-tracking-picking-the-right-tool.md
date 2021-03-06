---
title: "Persistent Location Tracking: Picking The Right Tool"
date: 2012-10-29
tags:
  - Location
  - Technical
layout: layouts/post.njk
---

In this post, I compare Google Latitude and InstaMapper, two popular services for persistent location tracking. I walk through installation and data extraction via API for each service, then provide some subjective first impressions as to which one better suits my location-tracking needs.

<!-- more -->

## Evaluating Tools

As the ecosystem of self-tracking tools [grows exponentially](http://quantifiedself.com/2011/03/the-state-of-quantified-self-a-year-of-growth/), choosing the right tool is becoming an increasingly daunting task. To add to the complexity of this decision, self-tracking tools are *highly personal.*

{% blockquote %}
How do I pick the best tool for me?
{% endblockquote %}

This question is far from monolithic:

- Do I want **manual** or **automatic** tracking?
  - How much *time and effort* am I willing to spend on self-tracking?
  - Is a hybrid *automatic plus manual annotation* approach workable?
- Do I want **persistent** tracking?
  - *All day?* Or only at predetermined times?
  - *Every day?* What if I'm on vacation?
- Do I want **raw data access?**
  - How do I want to access that data? Through *Excel CSV files?* Via a *developer-friendly API?*
  - What *granularity* do I want? Sub-second? Daily?
  - What *parameters* do I want? For location, is `(lat, long)` enough? Do I want *altitude* as well? GPS fix *accuracy?*

Without a *searchable database of self-tracking tools*, these questions can be difficult to answer. The main [Quantified Self website](http://quantifiedself.com/) includes a [Guide to Self-Tracking Tools](http://quantifiedself.com/guide/), but their implementation is subject to criticism:

{% blockquote "Robert Wood Johnson Foundation", "https://www.rwjf.org/content/dam/farm/reports/program_results_reports/2012/rwjf400733", "A Digital Guide for Self-Tracking Goes Online" %}
In a report to RWJF, Project Director Alexandra C. Carmichael noted that the guide was more a catalog of tools than a useful manual for people wanting to choose and use these tools.
{% endblockquote %}

This is a point worth repeating. Simply listing tools is *not enough*; a database of tools *must answer these basic questions* to be useful. A quick search on the Guide for [location-related tools](http://quantifiedself.com/guide/tag/location) comes up short:

<img src="https://lh6.googleusercontent.com/-1r1swg9oBxo/UJA_is6HMSI/AAAAAAAAAIQ/zoiBG4fRAPU/s640/qs-guide-location-apps.jpg" />

Why is [MoodPanda](http://moodpanda.com/) listed? I suppose it must location-tag mood entries, but *that isn't made explicit in the description.* [Momento](http://www.momentoapp.com/) makes a bit more sense, but it's primarily a journalling app. [Foursquare](https://foursquare.com/) is definitely location-based, but anyone unfamiliar with it *must read its description closely* to realize that it relies on manual check-ins.

In lieu of a useful tool database, the only effective option is direct evaluation. By investigating two popular location tracking tools, I'll demonstrate how such an evaluation might be carried out.

## The Tools

### Google Latitude

Google Latitude bills itself primarily as a social location sharing service:

<img src="https://lh5.googleusercontent.com/-ZGGebfguFEk/UJA_hShHXRI/AAAAAAAAAH4/kziP-01pI_g/s800/banner-glatitude.jpg" />

Social capacities aside, the [Location History](https://maps.google.com/locationhistory/b/0) functionality can be used as a persistent location-tracking tool.

### InstaMapper

I first heard of InstaMapper from [Ted Power's talk on geo-tracking](http://vimeo.com/8545134). Unlike Google Latitude, InstaMapper focuses more on personal tracking:

<img src="https://lh4.googleusercontent.com/-dOIGJWcJ7uc/UJA_h8QM2FI/AAAAAAAAAIA/0owDXIrD6Ro/s800/banner-instamapper.jpg" />

### The Criteria

My ideal location tracking tool is:

- **Android-compatible:** It should work with my [RAZR M](www.razr.com/RAZR-M) running [Android 4.0.4 (Ice Cream Sandwich)](http://www.android.com/about/ice-cream-sandwich/).
- **Battery-friendly:** It should allow me to go at least a day *without recharging.*
- **Automatic:** It should track my location *without requiring check-ins* or other manual input.
- **Persistent:** It should track my location *constantly.*
- **Fine-grained:** It should be capable of *per-minute resolution or better.*
- **Developer-friendly:** It should *provide an API* for fetching location history, and the data offered through that API should be *as complete as possible.*

Both tools are *Android-compatible*, *automatic*, and *persistent* already, which narrows down the list of criteria to evaluate.

## Installation

### Google Latitude

Enabling automatic location tracking on Android requires *only a single setting change:*

<img src="https://lh4.googleusercontent.com/-lGwyff6IKAQ/UJA_jzsY3CI/AAAAAAAAAIw/qgFZr8kT1xE/s288/install-glatitude-step1.jpg" />
<img src="https://lh5.googleusercontent.com/-v-7rvy4kAk4/UJA_kbfLddI/AAAAAAAAAI4/MLzFAjPXgR8/s288/install-glatitude-step2.jpg" />
<img src="https://lh3.googleusercontent.com/-rooAhkMibWg/UJA_kjz8o1I/AAAAAAAAAJA/sCnrK_yNHbE/s288/install-glatitude-step3.jpg" />
<img src="https://lh5.googleusercontent.com/-8jz3N_5HkUA/UJA_k6mNTAI/AAAAAAAAAJI/qerZyoCzXbo/s288/install-glatitude-step4.jpg" />

### InstaMapper

I followed the Android installation directions [here](http://www.instamapper.com/android_howto.html). After you [register for an InstaMapper account](https://www.instamapper.com/fe?page=register), you install InstaMapper's [GPS Tracker app](https://play.google.com/store/apps/details?id=com.instamapper.gpstracker&hl=en):

<img src="https://lh5.googleusercontent.com/-FJZ7CxlpWSE/UJA_lDw4OVI/AAAAAAAAAJQ/pCreIS9emn0/s288/install-instamapper-step1.jpg" />

### Comparison

Both tools are easily installed, but *Google Latitude* wins on simplicity. This is unsurprising, as Google Latitude comes pre-installed.

## Data Export

### Google Latitude

To export data from the Location History dashboard, click on *Export KML* under the calendar widget:

<img src="https://lh3.googleusercontent.com/-N_E7GC01k3I/UJA_lY310cI/AAAAAAAAAJY/B6qCcqCAPm0/s800/export-glatitude.jpg" />

### InstaMapper

Head to the *data page* for your device:

<img src="https://lh4.googleusercontent.com/-WiPRLpRcC9Q/UJA_l7UA-cI/AAAAAAAAAJg/ienRb1xYY2o/s400/export-instamapper-step1.jpg" />
<img src="https://lh4.googleusercontent.com/-kvWTFuAZoJ8/UJA_mK_zsbI/AAAAAAAAAJk/aG-iJs2Sfp8/s400/export-instamapper-step2.jpg" />

Here's where this process gets weird. To export your data, you first have to *define a track:*

<img src="https://lh3.googleusercontent.com/-0j8AdUIinoU/UJA_msnEnLI/AAAAAAAAAKM/LfOZOnEyOJA/s400/export-instamapper-step3.jpg" />
<img src="https://lh5.googleusercontent.com/-aiXmPGeKOxo/UJA_nRZr93I/AAAAAAAAAJ0/wWNddc34ZXo/s400/export-instamapper-step4.jpg" />
<img src="https://lh6.googleusercontent.com/-tgipa_V9TfU/UJA_ncU8LeI/AAAAAAAAAJ8/2HIvGJ_ycfY/s400/export-instamapper-step5.jpg" />

Once the track is created, you can *visit the Track Manager* to export your track data in a variety of formats:

<img src="https://lh6.googleusercontent.com/-OyteTDJcqYk/UJA_n7L2QvI/AAAAAAAAAKE/tvEkdMbB-Ik/s400/export-instamapper-step6.jpg" />
<img src="https://lh5.googleusercontent.com/-e52trEcnN0I/UJA_ob4XGgI/AAAAAAAAAKI/REcryQodFq0/s400/export-instamapper-step7.jpg" />

### Comparison

This one goes to *Google Latitude*. Aside from the terrible UI flow, InstaMapper has some other problems:

- The `accuracy` field is missing, making it harder to *filter out noisy readings.*
- As stated in the [InstaMapper FAQ](http://www.instamapper.com/faq.html), data access is *limited to the previous 30 days or 100 000 locations.*

## API Fetching

### Tailers and Streams

Many real-time APIs provide [REST](http://en.wikipedia.org/wiki/Representational_state_transfer) endpoints for fetching time-bounded chunks of data, such as
`https://www.googleapis.com/latitude/v1/location?key=INSERT-YOUR-KEY&min-time=1111&max-time=2222&max-results=10`.

By keeping track of a `since` time to fetch after, we can easily turn this into a stream:

```py
def request(since):
  # TODO: actually fetch data
  pass

def sleep(since, freq):
  elapsed = time.time() - since
  wait = freq - elapsed
  if wait < 0:
    return
  time.sleep(wait)

def poll(freq):
  since = time.time()
  while True:
    sleep(since, freq)
    locations = request(since)
    if not locations:
      continue
    doSomething(locations)
    since = locations[-1].timestamp
```

This pattern is often referred to as a *tailer.* Why? Suppose we have a simple implementation of `doSomething()`:

```py
def doSomething(locations):
  for location in locations:
    print location
```

This prints out locations as they are received, similar to UNIX `tail -F`. By adjusting `freq` I can make different real-time guarantees, although at some point the upstream API will start throttling my requests.

### Google Latitude

You can see a working tailer implementation [here](https://github.com/candu/quantified-savagery-files/blob/master/Location/tail_glatitude.py).

To access the [Google Latitude API](https://developers.google.com/latitude/), you first need to [register an application](https://code.google.com/apis/console/b/0/). This gives you the necessary parameters `YOUR_KEY`, `YOUR_SECRET` for stepping through the OAuth flow.

With the Python library [oauthclient2](http://code.google.com/p/google-api-python-client/wiki/OAuth2Client), retrieving OAuth credentials is relatively painless:

```py
from oauth2client.client import OAuth2WebServerFlow
from oauth2client.file import Storage
from oauth2client.tools import run

def getCredentials(key, secret):
  flow = OAuth2WebServerFlow(
    client_id=key,
    client_secret=secret,
    scope='https://www.googleapis.com/auth/latitude.all.best',
    redirect_uri='http://localhost:8080/oauth2callback'
  )
  storage = Storage('.creds')
  return run(flow, storage)
```

`oauth2client.tools.run()` invokes a browser window and starts an HTTP server to receive the OAuth callback. With the credentials, we can *make a signed API request:*

```py
import httplib2
import urllib
import json

def request(self, since):
  http = httplib2.Http()
  credentials = getCredentials(YOUR_KEY, YOUR_SECRET)
  credentials.authorize(http)
  url = 'https://www.googleapis.com/latitude/v1/location?%s' % urllib.urlencode({
    'max-results': 10,
    'min-time': since,
    'max-time': since + 10 * (15 * 1000),
    'granularity': 'best'
  })
  resp, content = http.request(url)
  data = json.loads(content)
  if data.get('error') is not None:
    return None
  return data['data'].get('items', [])
```

There are some minor details:

- The API *uses milliseconds for its timestamps*, so my `since` values take this into account.
- Without `max-time`, the API *returns the most recent* `max-results` locations. I supply a 150-second window.
- If there are no locations within the given time range, the API **does not** populate `data['data']['items']`. I use `get()` to work around the resulting `KeyError`.
- In the event of an error, the API populates `data['error']`. I use `None` as a *sentinel value* to indicate that an error has occurred.

### InstaMapper

You can see a working tailer implementation [here](https://github.com/candu/quantified-savagery-files/blob/master/Location/tail_instamapper.py).

InstaMapper doesn't use OAuth; instead, it uses a unique key `YOUR_KEY` that is passed as a GET parameter to the REST API:

```py
import httplib
import json
import urllib

def request(self, since):
  params = {
    'action': 'getPositions',
    'key': YOUR_KEY,
    'num': 10,
    'from_ts': since,
    'format': 'json',
  }
  url = 'http://www.instamapper.com/api?{1}'.format(APIHOST, urllib.urlencode(params))
  conn = httplib.HTTPConnection('www.instamapper.com')
  conn.request('GET', url)
  resp = conn.getresponse()
  if resp.status != 200:
    raise Exception('HTTP {0} {1}'.format(resp.status, resp.reason))
  data = json.loads(resp.read())
  conn.close()
  return data['positions']
```

### Comparison

Although InstaMapper's API is arguably simpler to use, I'll award this one to *Google Latitude:*

- **Security:** InstaMapper uses unencrypted HTTP GET requests, so anyone running a [packet sniffer](http://www.wireshark.org/) on my network has *complete access to my location data.* Google Latitude uses HTTPS and OAuth. No contest.
- **Support:** I can *leverage the community of Google API users* to help resolve any issues I encounter.
- **Data:** again, InstaMapper is *missing location accuracy.*
- **Request Volume:** InstaMapper permits one request every 10 seconds. Google Latitude allows 1 000 000 requests per day, or *one request every 0.0864 seconds.*

## Battery Usage

To find out how battery-friendly the two Android apps are, I *check the
Battery Manager:*

<img src="https://lh6.googleusercontent.com/-B246p7a_vbg/UJA_i7iGdyI/AAAAAAAAAIU/Q6U6hLdc2hg/s288/battery-overview.jpg" />
<img src="https://lh5.googleusercontent.com/-X6ClOm7t-8s/UJA_jVwjgrI/AAAAAAAAAIk/V1lOfjmpO2o/s288/battery-maps.jpg" />
<img src="https://lh5.googleusercontent.com/-r7N176E75z0/UJA_jdJfs_I/AAAAAAAAAIg/XQnPc0Q2lgY/s288/battery-gps-tracker.jpg" />

### Comparison

*Google Latitude* wins this one as well. InstaMapper keeps the GPS radio running almost constantly, whereas Google Latitude manages to sip radio access. I'm guessing that it uses WiFi, cell towers, and other non-GPS sources where possible.

Without these power consumption improvements, InstaMapper's GPS Tracker *uses an order of magnitude more energy* than Google Latitude. Ouch.

## First Impressions

After a day of persistent location tracking with both Google Latitude and InstaMapper, *Google Latitude wins hands-down.* It's *easy to install*, it provides *simple and secure data access* via `oauth2client`, and it *preserves battery life nicely.*
