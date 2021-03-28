---
title: "Applying Genetic Research To My 23andMe Data"
date: 2013-02-07
tags:
  - qs
  - technical
layout: layouts/post.njk
---

To calculate your risk of various diseases, 23andMe scours the medical research literature for studies that correlate incidence rates for those diseases with mutations at specific locations in the human genome. The locations where these mutations commonly occur are referred to as single-nucleotide polymorphisms, or [SNPs](http://en.wikipedia.org/wiki/Single-nucleotide_polymorphism).

In this post, I show how I applied the findings of [this study about caffeine-induced anxiety](http://www.nature.com/npp/journal/v33/n12/full/npp200817a.html) to discover more about myself. I have no genetic research background whatsoever, and my knowledge of genetics is minimal, so it's amazing that this is slowly becoming accessible to a wider audience.

<!-- more -->

## The Genetic Culprit

From the study abstract:

{% blockquote "Childs et al.", "https://www.nature.com/npp/journal/v33/n12/full/npp200817a.html", "Association between ADORA2A and DRD2 Polymorphisms and Caffeine-Induced Anxiety" %}
At the 150 mg dose of caffeine, we found a significant association between caffeine-induced anxiety (Visual Analog Scales, VAS) and ADORA2A rs5751876 (1976C/T), rs2298383 (intron 1a) and rs4822492 (3′-flank), and DRD2 rs1110976 (intron 6).
{% endblockquote %}

The SNPs `rs5751876`, `rs2298383`, `rs4822492`, and a few others are claimed here to relate to caffeine-induced anxiety. Reading further, [Figure 4](http://www.nature.com/npp/journal/v33/n12/fig_tab/npp200817f4.html#figure-title) and [Figure 5](http://www.nature.com/npp/journal/v33/n12/fig_tab/npp200817t4.html#figure-title) show *which variations are correlated with higher anxiety.* Here's a quick summary of the high-anxiety variations listed in those figures:

- `rs5751876`: T/T (vs. C/C, C/T)
- `rs2298383`: C/C (vs. T/T, C/T)
- `rs4822492`: C/C (vs. G/G, G/C)
- `rs1110976`: G/G (vs. G/-)

Armed with this information, I can check my own genome for variations at those SNPs.

## Checking My Genome

In the appendix of [this blog post](/posts/2013-02-04-the-behavioral-economics-of-23andme-results/), I discuss how to retrieve your genetic data from the 23andMe API. I followed those directions with two changes:

- I used the authorization scope `genomes`;
- I accessed the API endpoint `https://api.23andme.com/1/genomes/<id>`, where `<id>` is my internal ID. This ID is returned with every response from their API.

I downloaded the genomic data as `genome.json`:

```bash
curl https://api.23andme.com/1/genomes/<id>/ -H "Authorization: Bearer <access_token>" > genome.json
```

To help extract the specific SNPs listed above, I wrote
[a quick Python script](https://github.com/candu/quantified-savagery-files/blob/master/Genetics/extractSNP.py).
Running it, I get my results:

```bash
$ python extractSNP.py rs5751876 rs2298383 rs4822492 rs1110976 < genome.json
rs5751876       TT
rs2298383       CC
```

23andMe doesn't provide data on the `rs4822492` or `rs1110976` SNPs, but I can see that *I have the high-anxiety variations* at `rs5751876` and `rs2298383`.

The script uses 23andMe's [SNP list](https://api.23andme.com/res/txt/snps.data), which identifies the locations of all SNPs that they look for. The first time you run `extractSNP.py`, it will generate an index of all 23andMe SNPs in `.snps-index` to make subsequent runs faster. Once you have your `genome.json` data and have built the `.snps-index` index, *you can look up any SNP or group of SNPs in about a second.*

## Summary

To apply genetic research findings to your genomic data:

- Use the process described in [this blog post](/posts/2013-02-04-the-behavioral-economics-of-23andme-results/) with scope `genomes` and API endpoint `https://api.23andme.com/1/genomes/<id>` to download your genetic data. Save it as `genome.json`.
- Download [my script](https://github.com/candu/quantified-savagery-files/blob/master/Genetics/extractSNP.py) into the same folder as `genome.json`.
- Find a paper, journal article, etc. that mentions specific SNPs (those funny `rsXXX` or `iXXX` numbers).
- Run `python extractSNP.py rsXXX < genome.json` to search for those SNPs in your genome.

## Caveats

This is still a highly manual process, and you'll need some familiarity with the command line to pull it off. We haven't quite reached the promised near-future where the deepest insights about our personal genetics are easily available.

23andMe's data is incomplete: they only had two of the four listed SNPs. That said, it's far better than nothing!

Also, there's room for skepticism regarding the underlying research. Only 102 participants took part, all of European-American descent. The subjects all had stated caffeine intake levels of less than 300mg per day, or about 3 cups' worth - that's a pretty wide range of potential tolerances. Subjects rated their anxiety on a subjective scale. The researchers also took measurements of heart rate and blood pressure, but did not incorporate that data into the anxiety rankings.

No single study is perfect. For more reliable results, you'll want to dig up findings that are supported by multiple studies.
