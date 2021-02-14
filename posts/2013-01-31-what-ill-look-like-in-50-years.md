---
title: "What I'll Look Like In 50 Years"
date: 2013-01-31
tags:
  - Non-Technical
  - Technical
  - Computer Vision
layout: layouts/post.njk
---

I spent a few weeks in the not-so-frozen Canadian northlands over the winter
holidays. While there, I had the chance to visit an old childhood favorite:
the [Ontario Science Centre](http://ontariosciencecentre.ca/), six floors of science-based awesomeness.
One of their current exhibits, the [Amazing Aging Machine](http://ontariosciencecentre.ca/aging/), uses a
computer vision software package called [APRIL](http://aprilage.com/) to predict how your
face will change over the next 50 years.

In this post, I explore my results from that exhibit alongside a customized
aging I performed using the [APRIL API](http://www.aprilage.com/AprilAPI_V2.pdf).

<!-- more -->

## Present Me

It's not the most flattering photo, but here I am at 26:

<img src="https://lh4.googleusercontent.com/-8qaAivSLFrI/UQrbKiU3JZI/AAAAAAAAARY/9e7IvKZUB00/s288/aging1.jpg" />

## Future Me

### Take One: Amazing Aging Machine

First, my face balloons out massively:

<img src="https://lh4.googleusercontent.com/-LCFkNNtDiJg/UQrbKwGOIQI/AAAAAAAAARg/SS9o98axBtU/s288/aging2.jpg" />

Next, my cheek bones set downwards:

<img src="https://lh5.googleusercontent.com/-VZhuI1uOVQk/UQrbLTKdBXI/AAAAAAAAARo/LHKV6cGEBGA/s288/aging3.jpg" />
<img src="https://lh6.googleusercontent.com/-aNcc-FC_4yk/UQrbL53IPpI/AAAAAAAAARs/DRf3ySCxPs4/s288/aging4.jpg" />

Finally, my face leans up and wrinkles a tiny bit:

<img src="https://lh6.googleusercontent.com/-F8xBzpDWsM4/UQrbMUOukwI/AAAAAAAAAR0/cRqPDd_wYPM/s288/aging5.jpg" />

### Take Two: APRIL API

For this run, I had access to the raw aging metadata, so I could see
exactly how old APRIL thought I was at each point in the aging sequence.

From 26 to 28, there's not much change:

<img src="https://lh6.googleusercontent.com/-u36fDGLeI0Y/UQrbNrKtZyI/AAAAAAAAASE/NQSn0Y5uCng/s288/age28.jpg" />

Then, by age 35, my face elongates slightly:

<img src="https://lh4.googleusercontent.com/-cRxKskiAyos/UQrbOiA_OjI/AAAAAAAAASM/GBFlRfZtXnc/s288/age35.jpg" />

I while away the next couple of decades in relative facial stasis. The
most pronounced change is in my skin, which pales gradually with age:

<img src="https://lh6.googleusercontent.com/-gYCoSmKbBDw/UQrbO46gohI/AAAAAAAAASY/X8RoWKpGT_8/s288/age47.jpg" />
<img src="https://lh6.googleusercontent.com/-dWkaa-neumY/UQrbPgkBVtI/AAAAAAAAASg/ebWh4i14qYk/s288/age55.jpg" />

Finally, age catches up with me, and I wrinkle into a haunted
septuagenarian:

<img src="https://lh5.googleusercontent.com/-JNBO6QMu-Xg/UQrbP9uzUUI/AAAAAAAAASo/Dj43_1l46Zo/s288/age61.jpg" />
<img src="https://lh4.googleusercontent.com/-w7zx8Ql3PnM/UQrbQO2pqVI/AAAAAAAAASw/9HJrW1EUz2c/s288/age67.jpg" />
<img src="https://lh5.googleusercontent.com/-RNgo0CglAjs/UQrbQtlY69I/AAAAAAAAAS0/OXD8Yqf63og/s288/age72.jpg" />

A few changes, each very minor, contribute to my forlorn expression over
these last three photos.

- The *eyes get slightly rounder*, as though they're welling up.
- *Wrinkling above the eyes* gives the impression of a furrowed brow.
- The face *elongates yet again*, creating a drawn expression.
- As part of the elongation of the face, the *mouth corners sag downwards*
  into the merest hint of a frown.

Note the lack of deep forehead and upper nose creases which normally
accompany the furrowed brow expression. The mere suggestion of it on the eyes
is enough to trigger our expression recognition! It's amazing how sensitive
we are to minute variations in facial muscle position.

### Summary

These images provide two divergent visions for my distant future:

<img src="https://lh6.googleusercontent.com/-F8xBzpDWsM4/UQrbMUOukwI/AAAAAAAAAR0/cRqPDd_wYPM/s288/aging5.jpg" />
<img src="https://lh5.googleusercontent.com/-RNgo0CglAjs/UQrbQtlY69I/AAAAAAAAAS0/OXD8Yqf63og/s288/age72.jpg" />

For comparison, here's my father in his late 50s, looking quite a bit happier:

<img src="https://farm4.staticflickr.com/3177/2828216200_5846e31c4a_z.jpg" />

## Why Were Those So Different?

{% blockquote "The Amazing Aging Machine", "http://ontariosciencecentre.ca/aging/" %}
...the machine uses state-of-the-art aging software developed in partnership with Aprilage Development Inc. of Toronto to add decades to the faces of 8-12 year olds.
{% endblockquote %}

The Amazing Aging Machine is calibrated for ages 8-12, likely to match
the Ontario Science Centre's target demographic. (Sadly, I couldn't find
detailed visitor demographic data!) In my case, this creates an awkward
puffy look: it's applying changes in facial structure through adolescence,
when much of our bone growth occurs.

By contrast, the APRIL API asks for your current age, allowing it to more
correctly calibrate its models. As a result, the second set of faces exhibits
relatively little change in shape.

## What Do I Get Out Of This?

Although my face is unlikely to match either of these faces at 72, this
experiment provides some insight into how our faces change with age. After
all, the APRIL face aging models are based on real face data. They represent
a sort of statistical average of the aging process.

Also, I get the vaguely warm feeling that comes with having contributed to our
[collective intelligence](http://vimeo.com/29052688). I provided APRIL
with a real age-labelled face, which will likely be used to help train future
models.

## Appendix: How To Use The APRIL API

For the more technically-minded, I've provided a quick walkthrough of the
API aging pipeline. For all the gritty details, consult the [API docs](http://www.aprilage.com/AprilAPI_V2.pdf).

Before starting, I highly recommend installing a tool like [jsonpp](https://github.com/jmhodges/jsonpp);
it makes it much easier to read API results.

The first step is manual: you need to register at [ageme.com](http://www.ageme.com/), then
click the confirmation link in your email.

<img src="https://lh5.googleusercontent.com/-wuu_sRDb7qQ/UQrtRmoofNI/AAAAAAAAATE/l7CAexc1_ZY/s400/ageme_register.jpg" />

The next step is uploading an image, but let's check first that the API
works by retrieving our user info:

```bash
$ curl http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/userInfo
{"result_code":0,"message":"Unauthorized"}
```

Oops! We haven't authenticated ourselves. The Authorization header uses a
brain-dead and highly insecure `base64` encoding:

```
$ python -c "import base64; print base64.encodestring('username:password')"
dXNlcm5hbWU6cGFzc3dvcmQ=
```

(Obviously this isn't my real username/password. Substitute yours above and
use the resulting `base64`-encoded string in the `Authorization` headers
below. I'll use this bogus value to illustrate the flow.)

With the correct header, we can try fetching the user info again:

```
$ curl -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/userInfo | jsonpp
{
  "uri": "http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com",
  "email": "savage.evan@gmail.com",
  "tokens": 0,
  "numOfAgings": 1,
  "role": "user"
}
```

Great! Now we can POST an image to the uploading endpoint with `curl`:

```
$ curl -F 'filename=aging1.jpg' -F 'image=@/Users/candu/Desktop/aging1.jpg' -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/images
```

Another manual step: before proceeding, you'll need to purchase a token on
the [ageme.com](http://www.ageme.com/) site. At time of writing, this cost $3.99; I looked for
active promotion codes, but couldn't find any.

<img src="https://lh6.googleusercontent.com/-co9vyFu4uJQ/UQrtSM1T8mI/AAAAAAAAATM/8ozrK3aiGjk/s400/ageme_buytokens.jpg" />

With your aging token purchased, you can now create an aging document. This
lets APRIL know your age and ethnicity, which helps it to select the
appropriate models for your particular aging sequence. It also identifies the
starting image of that sequence via the `imageId` returned during image upload.

```
$ curl -H 'Content-Type: application/json' -d '{"document": {"gender": "male", "age": 26, "name": "Evan", "ethnicity": "Caucasian"}, "imageId": 2371944}}' -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/documents
```

We're ready to run the aging process. There's a single method `detectMatchAge`
for performing all three steps, but I'll break it down into the component
steps here:

```
$ curl -X POST -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/pointDetection
$ while true; do curl -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/status; done
$ curl -X POST -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/match
$ while true; do curl -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/status; done
$ curl -H 'Content-Type: application/json' -d '{"sequenceType": "Max72", "sequences": [{"smoking": 0, "sunExposure": 0, "multiplier": 1}]}' -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/aging
$ while true; do curl -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/status; done
```

Note the `while` loops, which wait for each step to complete. Once all steps
are completed, we retrieve the aging results:

```
$ curl -H "Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/results > aging_results.json
$ cat aging_results.json | jsonpp | head -15
[
  {
    "uri": "http://www.ageme.com/AprilAPI/users/savage.evan@gmail.com/documents/2371973/results/76647",
    "status": "done",
    "sequenceType": "Max72",
    "sequences": [
      {
        "smoking": 0.0,
        "sunExposure": 0.0,
        "multiplier": 1.0,
        "images": [
          {
            "age": 26,
            "uri": "http://www.ageme.com/AprilAPI/images/IhLAo8Sp"
          },
```

Finally, I wrote a bit of [Python glue](https://github.com/candu/quantified-savagery-files/blob/master/Aging/fetch_aging.py) to fetch the URLs and name
them by age:

```py
import json
import sys
import urllib2

data = json.loads(sys.stdin.read())
images = data[0]['sequences'][0]['images']
for image in images:
  url = urllib2.urlopen(image['uri'])
  path = 'age{0}.jpg'.format(image['age'])
  with open(path, 'w') as f:
    f.write(url.read())
```

With this, we can fetch the images:

```
$ python fetch_aging.py < aging_results.json
```

And that's it! Most of the process uses `curl`, with minimal leaning
on Python for its `base64` module.
