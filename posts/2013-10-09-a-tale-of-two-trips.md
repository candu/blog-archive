---
title: "A Tale of Two Trips"
date: 2013-10-09
tags:
  - Non-Technical
  - Text Processing
  - Visualization
layout: layouts/post.njk
---

This summer, [Valkyrie](https://www.eecs.berkeley.edu/~valkyrie/) and I travelled through Eastern Asia.  We started with the Great Barrier Reef and rainforests near Cairns, then went onwards to Singapore, Vietnam, Cambodia, Malaysia, and Korea before spending three typhoon-stricken days holed up in Manila, Philippines.

As with our [bike trip](https://savageinternet.github.io/biketotheearth/), we kept a [daily journal](https://ramblelust.savageinter.net/) of our travels in blog form.  In this post, I visualize the two trips from our blog entries using some simple word count graphs.  These aren't the most sophisticated visualizations possible, but they provide a simple starting point to build upon in future blog posts.

<!-- more -->

First of all, it feels good to write another post!  The rapidly upcoming [Quantified Self 2013 Global Conference](https://quantifiedself.com/blog/announcing-the-2013-quantified-self-global-conference/) seemed like a good excuse to break seven months of blog neglect, so here I am.

I'll refer to these trips as *Bike to the Earth* and *Ramblelust* respectively, following the names of each trip blog.  Let's start with a look at the broadest of broad textual measures, word count.

## Word Count

How many words did we write for each trip?  How many per post, on average?

```bash
$ python global_word_count.py < BikeToTheEarth/posts_normalized.json
141329 words in 197 posts (717 words/post)

$ python global_word_count.py < Ramblelust/posts_normalized.json
61010 words in 86 posts (709 words/post)
```

Not much difference here.  What happens if we graph the word counts over time? Top is Bike to the Earth, bottom is Ramblelust.

<img src="https://lh4.googleusercontent.com/-5Sv5_JZEDdw/UlcoazZGSxI/AAAAAAAAAks/9TZH7nDzpnQ/w1000/biketotheearth_daily_words.jpg" />
<img src="https://lh6.googleusercontent.com/-BW5K-iWb56c/UlcoZ4fktZI/AAAAAAAAAkw/3g2w4bbbMtI/w1000/ramblelust_daily_words.jpg" />

One point jumps out on the Bike to the Earth graph: [this post](https://savageinternet.github.io/biketotheearth/posts/2010/10/19/hellbania.html), a massive 3600-word whopper that details our arduous exit from the rain-stricken Albanian coastline and into Greece.  For comparison, our longest post from Ramblelust was [this one](https://ramblelust.savageinter.net/blog/2013/06/29/cam-ranh-ing-around/) about our CouchSurfing experiences in Cam Ranh, a short distance south from Nha Trang along the Vietnamese coast.

Still, it's hard to make much out of such noisy data.  Let's smooth that a bit by looking at weekly averages. Again, top is Bike to the Earth, bottom is Ramblelust.

<img src="https://lh6.googleusercontent.com/-9YT2XueNpAs/UlcodH_CpwI/AAAAAAAAAkk/0ZnCYmXSMJc/w1000/biketotheearth_daily_words_smoothed.jpg" />
<img src="https://lh4.googleusercontent.com/-C-Q604GWq84/UlcoesNibrI/AAAAAAAAAjk/8RHMmaBdOi0/w1000/ramblelust_daily_words_smoothed.jpg" />

Now another pattern pops out of the Bike to the Earth data: sometime around the beginning of September, our writing output doubled.  At that time, we were just entering Italy, where we were sandwiched in between the southern Alps and the sea for about 900km before reaching Rome.

As I go through this process, I'm constantly jumping back and forth between the blog posts and these graphs.  As with all visualization, this context is an essential part of understanding the data.

## Next Steps

There are lots of places we could go from here:

- sentiment analysis;
- location-based visualization (by combining with country data);
- authorship analysis (my posts vs. Valkyrie's posts)...

...the list goes on.  What would you like to see?  Comment via Facebook or Twitter to let me know, and I'll put it into the next blog post.
