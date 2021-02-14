---
title: "Fitbit: My Brief Experience"
date: 2012-10-16
tags:
  - Panic
  - Non-Technical
layout: layouts/post.njk
---

In this post, I discuss my experiences using the popular
[Fitbit](http://www.fitbit.com/) fitness tracker.

<!-- more -->

## My Time With Fitbit

I started using the [Fitbit Ultra](http://www.fitbit.com/product) on April 11, 2012:

<img src="https://lh6.googleusercontent.com/-BbdI4RDLEPg/UH4U2PwH7AI/AAAAAAAAAFI/cdY5hnwl3so/s400/steps-april.jpg" />

Over the following three months, I walked, ran, and otherwise jostled my Fitbit
about a good deal:

<img src="https://lh6.googleusercontent.com/-Rk-sPLHtYVg/UH4U3FhjRJI/AAAAAAAAAFY/J7Ygbqqfi_k/s288/lifetime-steps.jpg" />
<img src="https://lh4.googleusercontent.com/-663jKpbc6yw/UH4U3vzf8EI/AAAAAAAAAFg/-EnTuoTD9LQ/s288/lifetime-floors.jpg" />
<img src="https://lh4.googleusercontent.com/-yzUccJOlbCQ/UH4U36eSCJI/AAAAAAAAAFk/Qmx-r-swHwc/s800/lifetime-distance.jpg" />

Somewhere around July 12, tragedy struck: *I lost my Fitbit.*

<img src="https://lh3.googleusercontent.com/--zc0squq1yo/UH4U1nCGuQI/AAAAAAAAAE8/aDOP5c1f0pw/s400/steps-july.jpg" />

### The Good

My initial impression was ecstatic. Fitbit didn't look like your average
pedometer:

<img src="https://lh5.googleusercontent.com/-eLa1uqTeKRg/UH4U5G5GSNI/AAAAAAAAAF0/RiNA89GciGQ/s288/fitbit.jpg" />
<img src="https://lh5.googleusercontent.com/-eRCIrQhA5Kk/UH4U1SaRsKI/AAAAAAAAAE0/4y8n3UjOl-c/s288/janky-pedometer.jpg" />

{% pullquote %}
It was *small, sleek, easily concealed.* {" I felt like I'd stumbled upon the access
key to some secret cult of digerati hipster fitness fanatics. "} I could
flash my Fitbit, give a knowing nod - "yes, I too take an informed interest in my
personal health" - and be accepted into the ranks.
{% endpullquote %}

*Wireless syncing* and *long battery life* sweetened the deal. This was a vast step
up from my pen-and-paper recovery journal. I was doing *serious* self-tracking
with *serious* devices now.

As I started to use it, I noticed *small changes in my behavior.* I'd walk an
extra few blocks to the employee shuttle. I'd buy fewer groceries at the market,
forcing myself to walk there more frequently. I'd take late-evening walks if I
felt my daily step count was too low. Each change was minor, but they often
added up to *thousands of additional steps per day.*

I'd also revel in more extreme bursts of exercise. A hike in the Marin headlands
netted me the 30 000 step badge. I pocketed the 200 floors badge after a
[ride up to Tilden](http://goo.gl/maps/jB7fa).

For the first time, I could also see how much I was sleeping:

<img src="https://lh6.googleusercontent.com/-QGWtSgEdMz8/UH4U5qNFyXI/AAAAAAAAAF8/5dGzfE_2YBk/s400/sleep-graph.jpg" />

*Great gouts of data* poured into my life, chartporn galore for an unrepentant
math addict. Soon it even became a quasi-social activity as my leaderboard
filled up with my Fitbit-using friends.

All in all, the Fitbit seemed like a fantastic way to turbocharge my exercise
patterns.

### The Bad

My wife, [Valkyrie Savage](http://www.eecs.berkeley.edu/~valkyrie/), also had a Fitbit. In the instructions, women
were suggested to wear the Fitbit on their bra strap for the ultimate in
clandestine self-tracking. This soon unearthed a glaring problem:

{% blockquote %}
Sweat is corrosive to metal.
{% endblockquote %}

In particular, the internal leads started to corrode, and before long she was
unable to connect it to the base station. After a quick phone call, Fitbit
agreed to replace the device at no cost; we weren't the first users to have
this problem, and they were in the process of changing the documentation.

Still, the experience soured the deal a bit. Had they never field-tested it with
women?

While we waited for the replacement, I noticed something else: my wristband
had stretched out and was now loose on my wrist. This was a minor detail,
but it added to a growing concern that the Fitbit Ultra *might not be
durable enough to withstand our protracted Savage-ing.*

Her second Fitbit finally arrived, and we were back into the self-tracking groove.
We took our Fitbits everywhere: walking, running, playing soccer, cycling,
and...wait, no, *Valkyrie couldn't take it swimming.* Actually, it didn't
measure our cycling accurately, it was useless for my static
bodyweight exercises, and it couldn't track our occasional indoor climbing
stints effectively either. *It was discouraging us from doing the activities
we loved most!*

### The Ugly

As we kept up our co-tracking, Valkyrie and I noticed a curious effect.
There were several days where we spent the whole day together doing the
exact same things, and yet *I would always be 1000-2000 steps ahead.* Our stride lengths
and heights are nearly equal. What was going on?

We tried wearing the Fitbits in the same locations on our bodies. No effect.
We tried counting steps while we were out together. The counts matched up.
The solution came by accident. With the wristband getting more stretched out
by the day, I finally started taking my Fitbit off when going to bed.
going to bed.

Aha! There was the difference: *it was counting every tiny
movement I made while asleep.* This effect was never mentioned in the
manual. It hadn't occurred to us that *our data might not be comparable!*

Meanwhile, my interest in Quantified Self was gradually intensifying. I
decided to check out the [Fitbit API](http://dev.fitbit.com/), hoping to create something like
[zeo-crossfilter](https://github.com/beaugunderson/zeo-crossfilter) for Fitbit.
This immediately hit a snag: *to get the minute-by-minute data, you need
Partner API access.*

{% blockquote "Fitbit Partner API", "https://wiki.fitbit.com/display/API/Fitbit+Partner+API" %}
Partner API allows to fetch the intraday data points with 1 minute detail level for several user resources
{% endblockquote %}

Fortunately, [Pavel Risenberg](http://pavelrisenberg.com/)
happily extended this access upon request, and I soon had
[fitbit-crossfilter](https://github.com/candu/fitbit-crossfilter) up and
working.

<img src="https://lh6.googleusercontent.com/-Ys7TdGOf2kI/UH4U6Tb2pRI/AAAAAAAAAGE/yVHssco65NU/s640/fitbit-crossfilter.jpg" />

Again, though, there was that sour taste. *Why not provide this access by default?*
A bit of digging around the site revealed a likely culprit:
[Fitbit Premium](http://www.fitbit.com/premium/about).
Users can pay to turn Fitbit into a personal trainer, gaining access
to more powerful data reports and goal-setting tools.

### The Verdict

*Was the Fitbit useful for me?* As a way to encourage walking: definitely.
As a lightweight persistent self-tracking device: mostly. As part of an
exercise program that meant something to me: not really.

I was left with a strong suspicion that *I wasn't in their target demographic.* I was
already fairly active. 10 000 steps was more of a baseline than a goal. I didn't
really need to walk more, and *I couldn't trust it* to accurately track the types
of exercise I enjoy most.

This is an important lesson for aspiring Quantified Self entrepreneurs:

{% blockquote %}
Your product is personal by nature.
{% endblockquote %}

Your product will encounter
[different behaviors](http://quantifiedself.com/2012/08/nir-eyal-knowing-your-behaviour-type-from-gary-wolf-on-vimeo/),
needs, and goals. *You are not everyone.* You will never understand most of these
behaviors, needs, and goals firsthand. No amount of user studies,
A/B testing, or market research will save you from this fundamental truth.

The only way out is to *give users control.* Let them tinker, mashup, share,
and explore. *Let them decide what your product means to them.*

## Questions From My Time As A Fitbit User

### Who Owns Self-Tracking Data?

{% pullquote %}
Looking back, one of my largest complaints was about *closed-ness.* Part
of the Grand Promise of Quantified Self is *control over your data and how you
use it.* We're still a long way from that Grand Promise. {" We're in the Internet
Middle Ages, an era of data fiefdoms. "}
{% endpullquote %}

The analogy is apt. Much as the old fiefdoms laid claim to your land and labor,
these fiefdoms *use your data and your data entry labor to enrich
themselves.* Much as the old fiefdoms provided vital services in exchange
for this taxation, you receive the *benefit of services like search and
social networking.* Much as the old fiefdoms fought each other relentlessly for
economic gain, these fiefdoms *wage war over users and intellectual property.*

This is not necessarily bad. As a result of these data fiefdoms, we have many
services that might not otherwise exist. By selling your self-tracking data
back to you, Fitbit is *able to fund the provision of tools for managing and
improving your fitness.* Those tools are generally of reasonable quality,
and are likely to improve over time.

However, if you want to make your own tools, *you're largely out of
luck.* You can pay for different tools via Fitbit Premium, but there's no
guarantee that those tools will be better for *you.* Your only other
recourse is to navigate the API documentation and contact the right people for
better data access. Even with that access, you still only have
minute-by-minute data. You have no idea how Fitbit maps between raw
accelerometer readings and steps, and definitely no opportunity to improve that
mapping. To take my example, *I can't tweak the step detection algorithms to
measure cycling accurately.*

Even though the average person won't care to make these improvements,
*a few people will.* This recalls the [reddit maxim](https://www.facebook.com/photo.php?fbid=3563106890027):

<img src="https://lh6.googleusercontent.com/-Y4JWrp5wBmU/UH4U4dNSO-I/AAAAAAAAAFs/qCIibiyvafk/s400/give-a-damn.jpg" />

*There's a tension here.* This is how better products are built, but it's not
in Fitbit's interest to let just anyone do that in a completely unconstrained
fashion. If they do, they go out of business.

### What Is My Ideal Fitness Tracking Device?

It would be:

1. **activity-agnostic,** with the ability to track diverse forms of
   physical activity.
2. **water-resistant.** (I won't ask for waterproof, since I'm not much of a
   swimmer myself, but it should be able to handle light rain and a little
   sweat.)
3. **data-transparent,** allowing me to get at the raw data without going
   through a vendor API. (I note that [libfitbit](https://github.com/qdot/libfitbit) exists as an
   attempt to reverse-engineer Fitbit, but I haven't played around with it.)

I haven't looked into [BodyMedia](http://www.bodymedia.com/) or
[Fluxtream](https://fluxtream.com), but they both look promising.

### Is Persistent Tracking Useful?

{% blockquote %}
Yes, but only if you can analyze the data as quickly as you generate it.
{% endblockquote %}
