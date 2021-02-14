---
title: "Quadtree Cartography"
date: 2013-02-21
tags:
  - Non-Technical
  - Location
  - Visualization
layout: layouts/post.njk
---

In this post, I show off some images from a project I'm working on (which will
remain nameless for now!) These images visualize subdivisions of the Earth
into Google Maps tile-sized regions with roughly equal population. I'll also
provide a brief and non-technical rundown of the process by which I generated
these images.

<!-- more -->

## The Images

First, a representative image from my renderings:

<img src="https://lh5.googleusercontent.com/-EmN0ma8uhtg/USZnFkGsrfI/AAAAAAAAAV8/hDpa5sx1-IE/s640/tiles11.ag.jpg" />

I love working on problems with a visual aspect - you get direct sensory
feedback on your progress!

Here, we can clearly see the continents delineated
by dense coastal population clusters. India and China are especially detailed,
and Europe has fairly uniform density throughout. Contrast this with North
America: northern Canada is sparsely populated, as are the deserts and
mountains of the Central United States.

Next, some renderings at different subdivision levels (Google Maps zoom
levels 8-11):

<img src="https://lh4.googleusercontent.com/-SqLGYcz6yl0/USZnBXDoUNI/AAAAAAAAAUs/C7vdLkL522Y/s288/tiles8.ag60.jpg" />
<img src="https://lh5.googleusercontent.com/-m2wk-ov9Mw4/USZnBmDUucI/AAAAAAAAAU0/vrU48gzJei4/s288/tiles9.ag60.jpg" />
<img src="https://lh6.googleusercontent.com/-GuXnAIjWUf0/USZnCbAac_I/AAAAAAAAAU8/urh1UXBD3-U/s288/tiles10.ag60.jpg" />
<img src="https://lh6.googleusercontent.com/-Y53pPe7T0II/USZnCn5ZL3I/AAAAAAAAAVI/Owjf_pnQBic/s288/tiles11.ag60.jpg" />

As the subdivision level increases, the continents progress from blocky pixel
art to more recognizable shapes.

Finally, some renderings with different resolutions of the underlying population
data (degree, half-degree, quarter-degree, and 2.5 arc minutes):

<img src="https://lh6.googleusercontent.com/-GuXnAIjWUf0/USZnCbAac_I/AAAAAAAAAU8/urh1UXBD3-U/s288/tiles10.ag60.jpg" />
<img src="https://lh6.googleusercontent.com/-RRw5Gx4OiaA/USZnEQhqNhI/AAAAAAAAAVg/i6B3yx8BF_M/s288/tiles10.ag30.jpg" />
<img src="https://lh5.googleusercontent.com/-NkGpf7zzHsY/USZnFI4qQ7I/AAAAAAAAAV4/Kl1UB4U-4pU/s288/tiles10.ag15.jpg" />
<img src="https://lh6.googleusercontent.com/-n6Ufe_6mJzM/USZnF60IfvI/AAAAAAAAAWE/PEmAgvWvzNU/s288/tiles10.ag.jpg" />

Here the effect is more subtle: detail is added in densely populated areas,
but larger tiles (corresponding to more remote regions) are mostly unaffected.

To see all the images as small multiples, [view the album on Picasa](https://picasaweb.google.com/100933554722754572774/20130221QuadtreeCartography#).

## The Process

There are four major steps: getting the data, combining it with Google Maps
tile data, building the subdivision, and rendering it.

### Getting the Data

The [NASA Socio-Economic Data and Applications Center](http://sedac.ciesin.columbia.edu/citations),
or SEDAC, compiles global population grids. These grids contain the estimated
number of people living in each 2.5-arc-minute square of the Earth's surface.
2.5 arc-minutes is 1/24 of a degree, or about 4.5 km of equatorial circumference:
definitely high-resolution enough for building some awesome maps!

The population count grids are available [here](http://sedac.ciesin.columbia.edu/data/set/gpw-v3-population-count/data-download).
You have to register on the site and cite usage of their data, but otherwise it
appears to be freely available.

### Combining with Google Maps

Google Maps uses a [Mercator projection](http://en.wikipedia.org/wiki/Mercator_projection).
This projection is [truncated](https://developers.google.com/maps/documentation/javascript/maptypes#WorldCoordinates)
at roughly 85 degrees latitude to create a square map, which is then projected
onto a 256 x 256 world coordinate system. Finally, world coordinates are
mapped to [pixel coordinates](https://developers.google.com/maps/documentation/javascript/maptypes#PixelCoordinates)
at different zoom levels, which determine which [tile](https://developers.google.com/maps/documentation/javascript/maptypes#TileCoordinates)
your location falls in.

To match up the gridded population data with Google Maps tiles, then, we need
to do the following:

- for each grid cell, *determine its latitude and longitude boundaries*;
- use those boundaries to *figure out which map tiles the cell overlaps*;
- *divide the cell's population among those map tiles*.

To divide the cell's population fairly, I determine how much of the cell
overlaps each tile.

I found [this helpful example](https://google-developers.appspot.com/maps/documentation/javascript/examples/map-coordinates)
of working with locations, world coordinates, pixel coordinates, and tiles.
The source code of that example contains an implementation of Google's
Mercator projection, which I built into a larger [node.js](http://nodejs.org/)
utility for computing the equal-population subdivision.

(Yes, node.js is fine for CPU-intensive tasks, just not in the same process
as your webserver.)

### Building an Equal-Population Subdivision

To get map tiles of equal population, *I combine tiles into larger tiles
until the population exceeds a threshold.* This creates large tiles in
sparsely populated areas while leaving smaller tiles in densely populated
areas.

(I mentioned [quadtrees](http://blog.notdot.net/2009/11/Damn-Cool-Algorithms-Spatial-indexing-with-Quadtrees-and-Hilbert-Curves)
in the title of this post - this data structure is ideally suited for the
problem.)

### Rendering the Subdivision

This is the easy part! I used [Pillow](https://pypi.python.org/pypi/Pillow/), a
nicely-packaged version of the excellent [Python Imaging Library](http://www.pythonware.com/products/pil/),
to render the subdivisions out as JPEG images.

(I suppose I could have rendered SVG images in node.js using some [jsdom](https://github.com/tmpvar/jsdom)
and [d3](http://d3js.org/) hackery, but I was already familiar with using
Python Imaging Library for image synthesis.)
