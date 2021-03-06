---
title: "Financial Tracking: Mint Bubbles"
date: 2012-11-12
tags:
  - Financial
  - Technical
  - Visualization
layout: layouts/post.njk
---

In this post I present Mint Bubbles, a [force-directed bubble chart](http://www.nytimes.com/interactive/2012/02/13/us/politics/2013-budget-proposal-graphic.html) visualization of exported Mint data. I explain how to use [force-directed layouts](http://en.wikipedia.org/wiki/Force-based_algorithms_(graph_drawing)) to produce awesome interactive visualizations
with [d3](http://d3js.org/), and also provide details on some of the specific tricks used
to create Mint Bubbles.

<!-- more -->

## Getting Your Data

Exporting your data from Mint is easy. Log into Mint and go to the Transactions tab:

<img src="https://lh6.googleusercontent.com/-oHWRFHUK35A/UKLVzn8tlDI/AAAAAAAAAM4/_2mADDMZ__M/s640/transactions-tab-select.jpg" />

Scroll to the bottom pagination section. In barely-legible super-tiny type at bottom right, there's a link to export all your transactions:

<img src="https://lh3.googleusercontent.com/-VSYonXZ14ns/UKLVz3M9eHI/AAAAAAAAAMs/Svbd25tzd3A/s800/transactions-export-link.jpg" />

Clicking that link will download a file called `transactions.csv`:

<img src="https://lh6.googleusercontent.com/-iwz7B_kEtF8/UKLV0RLGvZI/AAAAAAAAAM0/w3tqQ53CVao/s800/transactions-csv-download.jpg" />

## Mint Bubbles

If you're viewing this on an RSS reader, check out the example [on my blog](/blog/2012/11/12/financial-tracking-mint-bubbles/#quick-demo). You will need a browser that supports the [HTML5 File API](https://developer.mozilla.org/en-US/docs/Using_files_from_web_applications).

You can see the code for this demo [here](https://github.com/candu/quantified-savagery-files/tree/master/Financial/mint-bubbles).

To see a visualization of your data, drag the `transactions.csv` file from Mint onto the `drag your data here` area below.

<div id="quick-demo" markdown="0">
  <style type="text/css">
    #quick-demo {
      line-height: 1;
    }

    #chart {
      height: 480px;
      width: 720px;
      margin: auto;
      margin-top: 32px;
      margin-bottom: 16px;
    }

    .chart-active {
      border: 1px solid #DFE2E1;
      background-color: #F7F7F7;
    }

    #drop_zone {
      display: table;
      border: 2px dashed #bbb;
      height: 100%;
      width: 100%;
      padding: 4px;
      cursor: pointer;
    }

    #drop_zone p {
      display: table-cell;
      vertical-align: middle;
      text-align: center;
      font-size: 150%;
      color: #7F7F7F;
    }

    .hidden {
      display: none !important;
    }

    circle.node {
      cursor: pointer;
    }

    circle.circle-active {
      fill: #36f !important;
      stroke: #03f !important;
    }

    #caption {
      width: 720px;
      margin: auto;
      text-align: center;
      min-height: 100%;
    }

    #total {
      font-size: 125%;
      color: #36f;
      padding: 4px;
      margin-bottom: 8px;
    }

    #prompt {
      font-size: 150%;
      color: #888;
      padding: 4px;
    }

    #transactions_table {
      width: 100%;
      margin-bottom: 8px;
    }

    #quick-demo th {
      font-weight: 500;
      padding-bottom: 4px;
    }

    #quick-demo th, #quick-demo td {
      text-align: center;
    }
  </style>
  <script src="https://candu.github.io/quantified-savagery-files/lib/js/third-party/mootools.js"></script>
  <script src="https://candu.github.io/quantified-savagery-files/lib/js/third-party/d3.js"></script>
  <script src="https://candu.github.io/quantified-savagery-files/Financial/mint-bubbles/demo.js"></script>
  <div id="chart">
    <div id="drop_zone">
      <p>
        drop your data here
        <div id="progress" class="hidden">
          <progress id="progress_bar"></progress>
        </div>
      </p>
    </div>
  </div>
  <div id="caption" class="hidden">
    <div id="prompt">
      click bubbles to see transaction details
    </div>
    <div id="total" class="hidden"></div>
    <div id="transactions" class="hidden">
      <table id="transactions_table">
        <thead>
          <tr>
            <th width="120px">Date</th>
            <th width="120px">Amount</th>
            <th width="480px">Description</th>
          </tr>
        </thead>
        <tbody id="transactions_tbody"></tbody>
      </table>
    </div>
  </div>
</div>

## Behind The Bubbles

### Inspiration

This visualization was inspired by the [NYT 2013 Budget Proposal Graphic](http://www.nytimes.com/interactive/2012/02/13/us/politics/2013-budget-proposal-graphic.html), which uses [d3.js](http://d3js.org/) to bring [Obama's 2013 budget proposal](http://www.whitehouse.gov/omb/budget) to life as an interactive bubble chart.

I'd just started using [Mint](https://www.mint.com/) for financial tracking, and this seemed like an awesome way to visualize my personal spending patterns. To help figure out the mechanics of the NYT visualization, I consulted [this article](http://vallandingham.me/bubble_charts_in_d3.html) by [Jim Vallandingham](http://vallandingham.me/). He explains in detail how to create similar visualizations using d3's [force-directed layouts](https://github.com/mbostock/d3/wiki/Force-Layout), which model your data as a set of particles moving about in space.

### Importing Data

Unlike my [previous](/blog/2012/10/22/dont-hate-cross-correlate/#quick-demo) [visualizations](/blog/2012/10/17/fitbit-apis-crossfilter-and-d3/#quick-demo), I wanted this visualization to allow you to play with your data. Enter the [HTML5 File API](http://www.html5rocks.com/en/tutorials/file/dndfiles/), which allows access to files via JavaScript. First, I set up the drag-and-drop listeners on `div#drop_zone`:

```js
/*
 * Octopress bundles ender.js, which provides $() for DOM access; mootools
 * tries to play nice, so it won't install its $() over that. I'm using
 * document.id() instead.
 */
var dropZone = document.id('drop_zone');
function trapEvent(evt) {
  evt.stopPropagation();
  evt.preventDefault();
}
dropZone.addEventListener('dragenter', trapEvent, false);
dropZone.addEventListener('dragexit', trapEvent, false);
dropZone.addEventListener('dragover', function(evt) {
  trapEvent(evt);
  // This makes a copy icon appear during the drag operation.
  evt.dataTransfer.dropEffect = 'copy';
}, false);
dropZone.addEventListener('drop', handleFileSelect, false);
```

`dragenter`, `dragexit`, and `dragover` are analogous to `mouseenter`, `mouseexit`, and `mouseover`. For those events, it suffices to call `trapEvent()`, which prevents the browser's default action from happening. For instance, Chrome on Mac OS will just download the `transactions.csv` file if you drag it into a browser tab, which is not what I want here.

`drop` is the interesting event:

```js
function handleFileSelect(evt) {
  trapEvent(evt);
  var f = evt.dataTransfer.files[0];
  // NOTE: you might want to filter out large or invalid files here.
  var reader = new FileReader();
  reader.onloadstart = function(e) {
    if (e.lengthComputable) {
      document.id('progress').removeClass('hidden');
      document.id('progress_bar').set('value', 0);
      document.id('progress_bar').set('max', e.total);
    }
  };
  reader.onprogress = function(e) {
    if (e.lengthComputable) {
      document.id('progress_bar').value = e.loaded;
    }
  };
  reader.onload = function(e) {
    document.id('caption').removeClass('hidden').addClass('chart-active');
    document.id('progress').addClass('hidden');
    document.id('drop_zone').addClass('hidden');
    document.id('chart').addClass('chart-active');
    buildChart(d3.csv.parse(e.target.result));
  };
  reader.readAsText(f);
}
```

This uses `FileReader.readAsText()` to read in the `transactions.csv` file, with `d3.csv.parse()` for turning that CSV file into a sequence of JavaScript objects representing the transactions. This parsing is triggered `onload`, which fires once file I/O has completed.

`onloadstart` and `onprogress` are used to monitor file I/O progress via the [HTML5 progress element](http://www.useragentman.com/blog/2012/01/03/cross-browser-html5-progress-bars-in-depth/) `document.id('progress_bar')`. Since `transactions.csv` files are typically small, and since the "uploading" is actually a client-local copy into browser memory, you'll probably never see that progress bar.

### Grouping Transactions

I group the transactions by category:

```js
var cs = {};
data.each(function(tx) {
  var c = tx['Category'];
  if (!(c in cs)) {
    cs[c] = {
      amount: 0,
      txs: []
    };
  }
  cs[c].amount += +(tx['Amount']);
  cs[c].txs.push(tx);
});
```

`amount` stores the total amount; note the use of `+(tx['Amount'])` to convert
CSV string values into numbers. `txs` is used for the transaction list.

I then convert these into nodes to be used by
`d3.layout.force()`:

```js
var nodes = [];
for (var c in cs) {
  nodes.push({
    R: Math.max(2, Math.sqrt(cs[c].amount)),
    category: c,
    amount: cs[c].amount,
    txs: cs[c].txs
  });
}
```

### Defining The Layout

Before building the visualization itself, I define a color gradient based on bubble radius, picking the colors using the excellent [Color Scheme Designer](http://colorschemedesigner.com/):

```js
var Rs = nodes.map(function(d) { return d.R; });
var minR = d3.min(Rs),
    maxR = d3.max(Rs);
var fill = d3.scale.linear()
  .domain([minR, maxR])
  .range(['#7EFF77', '#067500']);
```

Now on to the visualization. First, I need to create the [SVG element](https://developer.mozilla.org/en-US/docs/SVG):

```js
var w = 960, h = 480;
var vis = d3.select('#chart').append('svg:svg')
  .attr('width', w)
  .attr('height', h);
```

Next, I define the behavior and styling of the bubbles:

```js
var node = vis.selectAll('circle.node')
  .data(nodes)
  .enter().append('svg:circle')
  .attr('class', 'node')
  .attr('cx', function(d) { return d.x; })
  .attr('cy', function(d) { return d.y; })
  .attr('r', function(d) { return d.R; })
  .style('fill', function(d) { return fill(d.R); })
  .style('stroke', function(d) { return d3.rgb(fill(d.R)).darker(1); })
  .style('stroke-width', 1.5);
```

`fill(d.R)` uses the color gradient `fill` to make smaller bubbles lighter and larger bubbles darker.

As for the force-directed layout, I start with some basic properties:

```js
var force = d3.layout.force()
  .nodes(nodes)
  .links([])          // no edges between bubbles!
  .size([w, h])
  .gravity(0.05)      // controls speed at which bubbles seek the center
  .friction(0.95);    // slows down motion
```

### Tick Handler

{% blockquote "Mike Bostock", "https://github.com/mbostock/d3/wiki/Force-Layout#wiki-tick", "Force Layout" %}
`force.tick()`: Runs the force layout simulation one step.
{% endblockquote %}

Force-directed layouts model your data as a set of particles in space. Those particles are subject to various forces:

- **Gravity:** in d3, this is actually an attractive force pulling particles towards the center of the visualization.
- **Friction:** this slows down movement.
- **Tension:** if nodes are connected via links (edges), they will resist being moved apart.
- **Charge:** similar to electric charge, same-signed charges repel and opposite-signed charges attract.

A layout can describe some or all of these forces. Resolving the forces is a simple iterative process:

```js
while (true) {
  for (P in particles) {
    F = [0, 0];
    for (f in forcesActingOn(P)) {
      F[0] += f[0]; F[1] += f[1];
    }
    applyForceTo(P, F);
  }
}
```

In addition to the above forces, visualizations using `d3.layout.force()` can define their own forces via the `ontick` handler. I use this to apply two effects:

- **Size Sorting:** similar to [granular convection](http://en.wikipedia.org/wiki/Granular_convection), larger bubbles will rise while smaller bubbles sink.
- **Collision Detection:** I prevent bubbles from intersecting, since that makes it easier to select them.

```js
var floatPoint = d3.scale.linear()
  .domain([minR, maxR])
  .range([h * 0.65, h * 0.35]);

force.on('tick', function(e) {
  // vertical size sorting
  nodes.each(function(d) {
    var dy = floatPoint(d.R) - d.y;
    d.y += 0.25 * dy * e.alpha;
  });

  // collision detection
  var q = d3.geom.quadtree(nodes);
  nodes.each(function(d1) {
    q.visit(function(quad, x1, y1, x2, y2) {
      var d2 = quad.point;
      if (d2 && (d2 !== d1)) {
        var x = d1.x - d2.x,
            y = d1.y - d2.y,
            L = Math.sqrt(x * x + y * y),
            R = d1.R + d2.R;
        if (L < R) {
          L = (L - R) / L * 0.5;
          var Lx = L * x,
              Ly = L * y;
          d1.x -= Lx; d1.y -= Ly;
          d2.x += Lx; d2.y += Ly;
        }
      }
      // This short-circuits visit() for quadtree nodes that can't collide with
      // d1, resulting in O(n log n) collision detection.
      return
        x1 > (d1.x + d1.R) ||
        x2 < (d1.x - d1.R) ||
        y1 > (d1.y + d1.R) ||
        y2 < (d1.y - d1.R);
    });
  });
  node
    .attr('cx', function(d) { return d.x; })
    .attr('cy', function(d) { return d.y; });
});
```

### Alpha and Size Sorting

What's `e.alpha`? This is described cryptically in the [d3.js documentation](https://github.com/mbostock/d3/wiki/Force-Layout#wiki-start):

{% blockquote "Mike Bostock", "https://github.com/mbostock/d3/wiki/Force-Layout#wiki-start", "Force Layout" %}
Internally, the layout uses a cooling parameter alpha which controls the layout temperature: as the physical simulation converges on a stable layout, the temperature drops, causing nodes to move more slowly.
{% endblockquote %}

A look at the [code for d3.layout.force()](https://github.com/mbostock/d3/blob/master/src/layout/force.js#L46) provides some insight into what's happening here:

```js
force.tick = function() {
  // simulated annealing, basically
  if ((alpha *= .99) < .005) {
    event.end({type: "end", alpha: alpha = 0});
    return true;
  }
  // ...
}
```

Let's look at the size sorting code again:

```js
nodes.each(function(d) {
  var dy = floatPoint(d.R) - d.y;
  d.y += 0.25 * dy * e.alpha;
});
```

`floatPoint(d.R)` computes a "desired height" for the node `d`. The `d.y` adjustment moves `d` towards that height, using `e.alpha` to slow down the sorting adjustment as the layout "cools" into its final state.

### Collision Detection

The collision detection code is cribbed from [this page](http://mbostock.github.com/d3/talk/20111018/collision.html), which is part of a [talk](http://mbostock.github.com/d3/talk/20111018/#0) given by [Mike Bostock](http://bost.ocks.org/mike/) on d3.

## Up Next

I'm currently working on a post for the [main Quantified Self blog](http://quantifiedself.com/), in which I'm planning to feature another cool visualization for personal data. Aside from that, I'm hoping to use an upcoming post to dissect my Mint data in more detail. Keep posted!
