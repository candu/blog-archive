---
title: "datafist: Exploration And Analysis"
date: 2012-12-21
tags:
  - datafist
  - Non-Technical
layout: layouts/post.njk
---

In this post I introduce datafist, an in-browser tool for visually exploring
your data.

<!-- more -->

## First, A Quote

{% blockquote "Direct Manipulation Interfaces", "http://cleo.ics.uci.edu/teaching/Winter10/231/readings/1-HutchinsHollanNorman-DirectManipulation-HCI.pdf" %}
Are we analyzing data? Then we should be manipulating the data themselves; or if we are designing an analysis of data, we should be manipulating the analytic structures themselves.
{% endblockquote %}

## The Sixfold Path Of Self-Tracking

Self-tracking is a complex process. It can be broken down into stages:

- *Intent:* our initial goals or motivations in deciding to self-track.
- *Tools:* the devices or methods we use for tracking.
- *Measurement:* collecting our data using those tools.
- *Analysis:* extracting insights from our data.
- *Interpretation:* creating personal meaning from those insights.
- *Action:* responding to that personal meaning.

Thanks to smartphones and cheap sensors, many of us already have the tools
necessary for measurement. The psychology of intent and action is rapidly
being explored through [Habit Design](http://www.meetup.com/habitdesign/) and [Captology](http://captology.stanford.edu/), with
startups like [Lift](http://lift.do/) and [Beeminder](https://www.beeminder.com/) harnessing the findings
to great effect.

*What are the technologies of analysis and interpretation?*

### Visualization

Visualizations, even interactive ones, are usually designed to *answer
specific questions* such as [how did Obama win re-election?](http://www.nytimes.com/interactive/2012/11/07/us/politics/obamas-diverse-base-of-support.html)
Within the context of those questions, they help us understand our data
intuitively. Outside that context, however, they are often useless.

### Statistical/Mathematical Software

Environments like [R](http://www.r-project.org/) and [Mathematica](http://www.wolfram.com/mathematica/) allow you to *explore
your data in meticulous detail.* In the hands of people like
[Stephen Wolfram](http://blog.stephenwolfram.com/2012/03/the-personal-analytics-of-my-life/), they are the holy grail of data analysis. For the
less technically inclined, they remain hopelessly unintuitive.

## A Middle Road

What we need is *something between the two*, a hybrid that exposes the
exploratory power of the latter through the intuitive interface of the former.
Such a tool would give us the opportunity to *explore our data as we see fit.*
We could ask our data questions, iterating quickly on those questions until
we reach useful insights.

Until we can all converse with our data with the fluency of [Hans Rosling](http://www.ted.com/talks/hans_rosling_the_good_news_of_the_decade.html),
there's still room for improvement!

## datafist

datafist tries to bridge this gap by providing *visual and gestural actions*
for data manipulation. This is probably easier to demonstrate than describe,
so here's a screencast that shows an early development version of datafist
in action:

<div markdown="0">
  <iframe width="560" height="315" src="http://www.youtube.com/embed/ypitHPXKa8M" frameborder="0" allowfullscreen></iframe>
</div>

As you use datafist, *you're constantly modifying the analysis itself.*
This modification takes place through *visual and gestural actions:* you
move channels to the viewer, drag out ranges of time to zoom in on, and draw
regions around interesting clusters. As you do this, the view is
*updated in real-time*, allowing you to see the effects of your actions.

### Try datafist Out!

I'm hosting a version of datafist [here at savageevan.com](http://datafist.savageevan.com).
Note that this is still a very early development version!

### Contribute to datafist!

If you're interested in making datafist better, [fork me on github!](https://github.com/candu/datafist)
Bug reports should be submitted [via the issue tracker](https://github.com/candu/datafist/issues).
In particular, if you have a CSV file that won't import properly, please attach
it for testing purposes!

## Inspiration

- [AudioMulch](http://www.audiomulch.com/) is an awesome graphical audio synthesis tool.
- [PureData](http://puredata.info/) and [Max/MSP](http://cycling74.com/products/max/) are visual signal processing languages.
- [Direct Manipulation Interfaces](http://cleo.ics.uci.edu/teaching/Winter10/231/readings/1-HutchinsHollanNorman-DirectManipulation-HCI.pdf) is a classic paper on the design of
  natural-seeming interfaces. You'll recognize some of the interface concepts
  from the analysis package design mocks at the beginning.
- [FAKEGRIMLOCK](http://www.startuplessonslearned.com/2011/11/startup-is-vision.html) is a fountain of poorly-Englished wisdom on
  entrepreneurship.
