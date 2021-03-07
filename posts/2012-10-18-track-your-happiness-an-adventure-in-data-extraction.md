---
title: "Track Your Happiness: An Adventure In Data Extraction"
date: 2012-10-18
tags:
  - Panic
  - Technical
layout: layouts/post.njk
---

In this post, I go over my first report from [Track Your Happiness](https://www.trackyourhappiness.org/), a tool that uses the [Experience Sampling Method](https://www.trackyourhappiness.org/) for mood tracking.

<!-- more -->

## My Report

### Charts

My happiness is *relatively constant across days of the week.*

<img src="https://chart.googleapis.com/chart?chs=310x200&cht=bvg&chco=0088cc&chxt=x%2Cy&chxl=0%3A%7CSun%7CMon%7CTue%7CWed%7CThu%7CFri%7CSat&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Aolpkmkp&chbh=30" alt="Weekday" />

I'm *happiest at the gym or in parks*, with vacations and restaurants close behind. "At Home" is mid-pack, with *"At Work" near the bottom.*

<img src="https://chart.googleapis.com/chart?chs=310x338&cht=bhg&chco=0088cc&chxt=y%2Cx&chxl=0%3A%7CBus+Stoo%7CPlane%7CAt+Work%7CIn+A+Car%7CDentist%7CAt+Home%7CAirport%7CRestaurant%7CVacation%7CPark%7CGym&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Auusroonliee&chbh=20" alt="Location" />

*Fun, exercise, and food* generate the most happiness. *Passive actions* such as watching TV, commuting, and waiting rank much lower. *Work is least happiness-inducing.*

<img src="https://chart.googleapis.com/chart?chs=310x422&cht=bhg&chco=0088cc&chxt=y%2Cx&chxl=0%3A%7CWorking%7CCommuting%2C+Traveling%7CWaiting%7CWatching+Television%7CReading%7CHome+Computer%7CGrooming%2C+Self+Care%7CShopping%2C+Errands%7CRelaxing%2C+Nothing+Special%7CTalking%2C+Conversation%7CEating%7CPlaying%7CPreparing+Food%7CExercising&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Autrrrqpnnnmlkj&chbh=20" alt="What are you doing?" />

*Whether I want to perform a task* is a much stronger determinant of happiness than whether I have to:

<img src="https://chart.googleapis.com/chart?chs=310x200&cht=bvg&chco=0088cc&chxt=x%2Cx%2Cy&chxl=0%3A%7CDon%27t+want+to%7CWant+to%7CWant+to%7CDon%27t+want+to%7C1%3A%7CHave+to%7CHave+to%7CDon%27t+have+to%7CDon%27t+have+to&chxr=2%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10%7C2%2C666666%2C10&chd=s%3Agope&chbh=51" alt="Want to / Have to" />

I'm *happier when outside.*

<img src="https://chart.googleapis.com/chart?chs=310x126&cht=bhg&chco=0088cc&chxt=y%2Cx&chxl=0%3A%7CNo%7CYes&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Apj&chbh=40" alt="Outside?" />

I'm *happier when alone.*

<img src="https://chart.googleapis.com/chart?chs=310x126&cht=bhg&chco=0088cc&chxt=y%2Cx&chxl=0%3A%7CNo%7CYes&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Apl&chbh=40" alt="Alone" />

Given that, it seems counterintuitive that *I'm happier when interacting with multiple people.*

<img src="https://chart.googleapis.com/chart?chs=310x132&cht=bhg&chco=0088cc&chxt=y%2Cx&chxl=0%3A%7CThree+Or+More%7CTwo%7COne&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Aorq&chbh=26" alt="Number of people interacting with" />

I was also surprised by this one: I'm happiest when *talking with acquaintances or friends* and least happy when *talking with family.*

<img src="https://chart.googleapis.com/chart?chs=310x198&cht=bhg&chco=0088cc&chxt=y%2Cx&chxl=0%3A%7COther+Relatives%7CSpouse%2FPartner%2FSignificant+Other%7CStrangers%7CCo+Workers%7CFriends%7CAcquaintances&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Autsrpo&chbh=20" alt="Who talking with" />

### What Does It Mean?

Even without considering the specific results, I have a few *unanswered questions:*

- What is *happiness*? How do I judge it at a particular moment? Is my judgment *accurate and consistent?*
- Is it necessarily better to be happier, or is there a threshold past which additional happiness doesn't improve the quality of life?
- Are these results *significant?* They're computed from just 50 samples, which seems low for drawing such broad conclusions.
- Do these activities make me more or less happy, or *do these readings reflect my pre-existing mental state?*

There's also the issue of those surprising findings. Am I really less happy when talking with [Valkyrie Savage](http://www.eecs.berkeley.edu/~valkyrie/)? To me, the most likely explanation is *trust*: around her, *I feel free to discuss negative aspects of my life.* Doing so would necessarily involve fixating on those aspects, which could account for some happiness reduction.

During this period, I was confronting *doubt and frustration in my job.* According to my personal data, I was also [drinking heavily](/posts/2012-10-08-self-tracking-for-panic-a-deeper-look/), possibly as a means for coping with that negative emotion. (It doesn't help.) Guilt is a potential factor; perhaps I felt that I was always offloading that doubt and frustration onto her.

The problem, though, is that *none of these explanations are testable*. They seem reasonable to me, but from a scientific standpoint they *fail a simple criterion:*

{% blockquote %}
Upon viewing only my data, would an impartial stranger reach similar conclusions?
{% endblockquote %}

I can't see how they would, since *my explanations involve intricate self-knowledge* that is not represented in the data.

### A Further Note On Significance

Let's take a more critical look at this chart:

<img src="https://chart.googleapis.com/chart?chs=310x198&cht=bhg&chco=0088cc&chxt=y%2Cx&chxl=0%3A%7COther+Relatives%7CSpouse%2FPartner%2FSignificant+Other%7CStrangers%7CCo+Workers%7CFriends%7CAcquaintances&chxr=1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3Autsrpo&chbh=20" alt="Who talking with" />

I mentioned that this data was drawn from a total of 50 samples. I'm assuming that these bars represent *average reported happiness* in each category. But:

- **Which average?** Probably the mean, but that's not made explicit anywhere.
- **Where are the error bars?** I have no idea whether the ranking is significant.
- **How many samples go into each bar?** Maybe "Acquaintances" and "Other Relatives" are outliers because I rarely talk to people in those categories.

This leads to an important point:

{% blockquote %}
Never present uncertain information as certain.
{% endblockquote %}

## Digging Deeper

Consider this chart:

<img src="https://chart.googleapis.com/chart?chs=310x200&cht=s&chco=0088cc&chxt=x%2Cy&chxr=0%2C0%2C100%7C1%2C0%2C100&chxs=0%2C666666%2C10%7C1%2C666666%2C10&chd=s%3AaUXKPnmomsWw0tSQnXaVrk%2CslrjjuZtXvZotualhrmepm" alt="Focused" />

*Am I happier when I'm more focused?* It's hard to tell from looking at this chart. This is a prime use case for *linear regression*, but I don't have the data! They [claim to have plans for data export](http://support.trackyourhappiness.org/customer/portal/questions/302357-combine-categories-), but I haven't seen those come to fruition. What now?

### Data Extraction

Fortunately, the chart was generated using the (now deprecated) [Image Charts](https://developers.google.com/chart/image/) functionality of the [Google Charts API](https://developers.google.com/chart/). With Image Charts, you *make requests to specially encoded URLs:*

```bash
https://chart.googleapis.com/chart
  ?chs=310x200
  &cht=s
  &chco=0088cc
  &chxt=x%2Cy
  &chxr=0%2C0%2C100%7C1%2C0%2C100
  &chxs=0%2C666666%2C10%7C1%2C666666%2C10
  &chd=s%3AaUXKPnmomsWw0tSQnXaVrk%2CslrjjuZtXvZotualhrmepm
```

You can see what all those parameters do [here](https://developers.google.com/chart/image/docs/chart_params), but the one I really care about is `chd`. This *encodes the chart data* in the [Simple Encoding Format](https://developers.google.com/chart/image/docs/data_formats#simple). I'll walk through *how to decode this data.*

As it stands, the value of `chd` is [URL-encoded](http://tools.ietf.org/html/rfc3986#section-2.1). We need to decode those `%3A` and `%2C` escape sequences.

```py
import urlparse
params = urlparse.parse_qs('chd=s%3AaUXKPnmomsWw0tSQnXaVrk%2CslrjjuZtXvZotualhrmepm')
chd = params['chd'] # 's:aUXKPnmomsWw0tSQnXaVrk,slrjjuZtXvZotualhrmepm'
```

The `s:` at the front means *use the simple encoding*. In that encoding, the characters `A-Za-z0-9` are mapped to values 0-61 in a, well, simple manner:

```py
def _get_simple_value(c):
  if c == '_':
    return None
  if 'A' <= c <= 'Z':
    return ord(c) - ord('A')
  if 'a' <= c <= 'z':
    return 26 + ord(c) - ord('a')
  if '0' <= c <= '9':
    return 52 + ord(c) - ord('0')
  raise ValueError('invalid character for simple encoding: {0}'.format(c))
```

Here the underscores `_` indicate missing or `null` values. With this function, recovering the original data from the `chd` param is a quick one-liner:

```py
data = [map(_get_simple_value, s) for s in chd[2:].split(',')]
```

By default, the simple encoding maps onto an effective range of 1-100, so the last step is to normalize this and `zip()` the lists into pairs:

```py
def fitSimpleToRange(x, xmin, xmax):
  if x is None:
    return None
  nx = x / 61.0
  return (1.0 - nx) * xmin + nx * xmax

points = zip(
  [fitSimpleToRange(x, 0, 100) for x in data[0]],
  [fitSimpleToRange(y, 0, 100) for y in data[1]]
)
```

Done! I've packaged this up as [chdecode](https://github.com/candu/quantified-savagery-files/blob/master/lib/py/chdecode.py), which also deals with the [Basic Text](https://developers.google.com/chart/image/docs/data_formats#text) and [Extended Encoding](https://developers.google.com/chart/image/docs/data_formats#extended) formats.

### Let's See Those Charts Again

You can see the code for this analysis [here](https://github.com/candu/quantified-savagery-files/blob/master/Panic/track-your-happiness/linregress.py).

Focus, productivity, and sleep quality all have *minor positive correlations* with happiness:

<img src="https://lh4.googleusercontent.com/-DG51p79XNtk/UIGcRjGMLQI/AAAAAAAAAG4/mk1xaar0yJM/s640/happiness-focus.jpg" alt="Focus" />
<img src="https://lh6.googleusercontent.com/-85nu0a-MBJw/UIGcRyutW9I/AAAAAAAAAG8/psRbjq12PLw/s640/happiness-productivity.jpg" alt="Productivity" />
<img src="https://lh3.googleusercontent.com/-bjcS4-21xIw/UIGcSLK9mCI/AAAAAAAAAHA/EVJ1qonZvks/s640/happiness-sleep-quality.jpg" alt="Sleep Quality" />

The *most significant one is focus,* but with $ p = 0.0927 $ it doesn't quite make the 5% significance threshold.

## Up Next

This ends my series of posts on data collection and analysis for dealing with panic disorder. In my next few posts, I'll talk about my plans for future experiments.
