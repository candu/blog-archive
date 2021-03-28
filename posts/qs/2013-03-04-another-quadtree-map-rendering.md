---
title: "Another Quadtree Map Rendering"
date: 2013-03-04
tags:
  - qs
  - nonTechnical
  - dataviz
layout: layouts/post.njk
---

This will be a quick post: I've got another population-based map rendering to
share, based on the work described in [this post](/posts/2013-02-21-quadtree-cartography/).

<!-- more -->

## The Rendering

This rendering uses tiles at Google Maps zoom level 14:

<img src="https://lh5.googleusercontent.com/-74zVhVDHIdc/UTVAtI4bhcI/AAAAAAAAAWY/sWT9JplWl7k/s800/tiles14.2048.jpg" />

I decided to experiment with solid shading rather than wireframe for the tiles.  This cuts down on the [Moiré effect](http://en.wikipedia.org/wiki/Moir%C3%A9_pattern) in densely populated areas.

The original is a *whopping 1 gigapixels*, so I had to resize it using [ImageMagick](http://www.imagemagick.org/script/index.php) before uploading it to Picasa:

```bash
$ convert tiles14.jpg -sample 2048x2048 tiles14.2048.jpg
```

A few more random tidbits of information:

- Computing the tile subdivision *took one CPU-hour* on my laptop, a fairly new MacBook Air.
- At zoom level 14, tiles near the equator are *roughly 1.5 miles to a side.* (Tiles further north or south are shorter in the north-south direction due to distortion in the Mercator projection.)
- *The Nile is clearly visible* between the Nile Delta and Aswan.

## Next Post

In my next post, I'll dive into [six months of journal entries](https://savageinternet.github.io/biketotheearth/) from a [six-month bike trip](http://goo.gl/maps/0Xs55) that [Valkyrie Savage](http://www.eecs.berkeley.edu/~valkyrie/) and I took back in 2010.
