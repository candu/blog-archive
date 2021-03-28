---
title: "Sober Thoughts On Willpower And Decision Making"
date: 2012-11-14
tags:
  - qs
  - nonTechnical
layout: layouts/post.njk
---

In this post, I discuss my ongoing experiment with temporarily eliminating alcohol from my diet. I use this experience to address a question: why do we find some forms of habit change easier than others?

<!-- more -->

## Background

As of today, *I've been completely sober for over a month.* I took my last drink at [Seven's Ale House](http://goo.gl/maps/nSxLn) on October 13 with these fine folks:

<img src="https://lh6.googleusercontent.com/-chtv-noAeXM/UKQNQdVUz1I/AAAAAAAAANQ/8zTq_kKfbCU/s640/sevens-pub.jpg" />

Why did I decide to do this? One of the takeaways from my [self-tracking for panic](/posts/2012-10-14-self-tracking-for-panic-another-dataset/) was that *I drink heavily and frequently:* about three drinks per day, six days per week. The USDA recommendations are somewhat stricter:

{% blockquote "Center for Nutrition Policy and Promotion", "https://www.cnpp.usda.gov/Publications/DietaryGuidelines/2010/DGAC/Report/D-7-Alcohol.pdf", "Dietary Guidelines for Americans" %}
..."low-risk" drinking [is defined] as no more than 14 drinks a week for men and 7 drinks a week for women with no more than 4 drinks on any given day for men and 3 drinks a day for women.
{% endblockquote %}

[This online questionnaire](https://alcoholscreening.org/page-q1-a/) put my drinking level in context:

{% blockquote "Center on Addiction", "https://alcoholscreening.org/page-q1-a/", "Online Quiz" %}
Many of us think our drinking is like everyone else's.  In fact, less than 10% of the general adult American population and 16% of males drink more drinks each week than you told us you drink.
{% endblockquote %}

*How much does the average American drink?* Using the data from [this Wikipedia article](http://en.wikipedia.org/wiki/List_of_countries_by_alcohol_consumption) and some simple calculations:

```py
# 1 drink = 1 beer bottle (355mL, 5% abv)
ALC_PER_BEER = 0.355 * 0.05
# American consumption = 9.44 L/year
DRINKS_PER_YEAR = 9.44 / ALC_PER_BEER
# 1 year = 365 days
DRINKS_PER_DAY = DRINKS_PER_YEAR / 365
print DRINKS_PER_DAY
# prints: "1.3027204321821337"
```

About $ 1.3 $ drinks per day, or roughly half of what I was drinking during my two panic tracking periods. If you ask [Gallup](http://www.gallup.com/poll/156770/majority-drink-alcohol-averaging-four-drinks-week.aspx), though, they have a different number: $ 4.2 / 7 = 0.6 $ drinks per day. [Rethinking Drinking](http://pubs.niaaa.nih.gov/publications/RethinkingDrinking/Rethinking_Drinking.pdf), a pamphlet from the [National Institutes of Health](http://www.nih.gov/), provides yet another look at drinking habits nationwide:

<img src="https://lh3.googleusercontent.com/-vEbziueqO8I/UKQN1vuM15I/AAAAAAAAANg/ermiP-4-0oA/s800/nih-alcohol-use.jpg" />

(This points out a general problem with data in the social sciences. Polling and measurement methodologies vary widely, as do the means by which data is presented.)

Regardless of which source I choose to believe, *my data still places me above average.*

There was also a more personal reason: in [analyzing the panic data](/posts/2012-10-09-self-tracking-for-panic-an-even-deeper-look/), *I found that caffeine wasn't the only panic-inducing culprit.* By training a [maximum entropy classifier](https://github.com/candu/quantified-savagery-files/blob/master/Panic/recovery-journal/panic_maxent.py), I found that high alcohol consumption was predictive of panic attacks. [Dissecting my data with bash](/posts/2012-10-08-self-tracking-for-panic-a-deeper-look/) supported this hypothesis: on days where I had a panic attack, I was usually drinking more than average both that day and the previous day.

## Elimination Or Moderation?

So why elimination instead of moderation? Simple: *moderation wasn't working.* I'd been using the USDA guidelines as my goal during the two panic tracking periods, with little success.

(As it happens, I was also reading [Big Sur](http://www.emptymirrorbooks.com/beat/kerouac-big-sur.html) at the time, which contains [Jack Kerouac's](http://www.jackkerouac.com/) harrowing account of [delirium tremens](http://www.ncbi.nlm.nih.gov/pubmedhealth/PMH0001771/). This may have provided some additional impetus in the decision!)

The [received wisdom](http://strategicsimplicity.com/3-reasons-to-form-new-habits-slowly-and-how-i-failed) is that this sort of "cold turkey" habit change usually leads to failure: willpower is finite, we burn out easily, there are powerful social triggers, etc. Except:

{% blockquote %}
I didn't find elimination harder. On the contrary, it was much easier than moderation.
{% endblockquote %}

I didn't stop going out to bars or visiting friends. I didn't smash all the bottles in the liquor cabinet or pour out the homebrew stash. I didn't enroll in any support groups or 12-step programs. What gives?

## Willpower: Endurance Versus Strength

Elimination and moderation have different *decision-making profiles:*

- **Elimination:** the decision is always No. This default decision is applied to every decision instance.
- **Moderation:** the decision may be Yes or No. Each decision instance requires a consideration of the circumstances.

When I attempted to apply moderation, I found myself *breaking down this consideration into a complex set of rules:*

- **Amount:** *Have I said Yes too much?*
- **Cost:** *Who pays for Yes?* Am I paying? Is a friend buying the next round? Did I receive free beer in exchange for volunteer services?
- **Novelty:** *Is this Yes different somehow?* Am I at a brewery I'll likely never visit again? Did a batch of homebrew just finish carbonation?
- **Social Pressure:** *What are the social costs of Yes and No?*
- **Special Occasions:** *Does the occasion warrant changing the Yes threshold?* Am I on vacation? At a fancy restaurant? Out at a concert?

Taking the [willpower as muscle](http://scopeblog.stanford.edu/2011/12/29/a-conversation-about-the-science-of-willpower/) metaphor one step further, this was a feat of endurance. Even though amount should be the only relevant factor here, *each decision instance spawned a host of smaller sub-decisions.*

By contrast, the elimination strategy required only one decision for each instance, *and that decision was predetermined:* No. It was a larger single decision, more akin to a feat of willpower strength.

## Replacing The Routine

In [Charles Duhigg's](http://charlesduhigg.com/) conception of the [habit loop](http://charlesduhigg.com/how-habits-work/), we can't truly break habits; we can only *swap in alternate routines* that connect the old cues and rewards.

This reminded me of a term my friend [Travis Brooks](http://www.linkedin.com/pub/travis-brooks/4/668/b44) used: EANAB, short for *Equally-attractive Non-Alcoholic Beverage.* There are delicious [flavor syrups](http://shop.torani.com/Bacon-Flavored-Syrup/p/TOR-431248&c=Torani@Syrups?utm_source=google&utm_medium=cpc&adtype=pla&kw=&gclid=CNL6sv21z7MCFQuCQgod-RcAgA) and [ginger beers](http://www.bundaberg.com/info/product_range/ginger_beer/). [Spa water](http://www.myrecipes.com/recipe/herb-infused-spa-water-10000000682668/) and [carbonation systems](http://store.primowater.com/Carbonators.aspx) lend new life to boring [dihydrogen monoxide](http://www.dhmo.org/facts.html). By making non-alcoholic beverages *as exciting as microbrews and Sonoma wines*, I tapped into my desire for exploration: here was a whole new range of beverages to discover!

## Openness And Social Myths

As the Alcohol Screening questionnaire said:

{% blockquote %}
Many of us think our drinking is like everyone else's.
{% endblockquote %}

While it is true that [more educated people drink more](http://www.psychologytoday.com/blog/the-scientific-fundamentalist/201010/why-intelligent-people-drink-more-alcohol), I encountered much less of a "drinking culture" among my friends than I had expected. In fact, by being open about my behavior change and the motivations behind it, I received a good deal of social support for this decision.

*Mistaken expectations are persistent in habit change:*

- **Fear Of Isolation:** We may believe that our current habits are *normal or average*, and resist changing for fear of being regarded as unusual.
- **Fear Of Inadequacy:** We may believe that we are *unable or less able* to change than others, and resist changing for fear we will not be successful.

In both cases, data to refute the fear-expectation may be hard to find.

## Final Thoughts

There are many ways in which my approach *could fail to work for others:*

- **Physical Dependence:** Although I drank more than average, my drinking had not progressed to the point of chronic dependence. Alcohol withdrawal [can be extremely serious](http://www.ncbi.nlm.nih.gov/pubmedhealth/PMH0001769/), so this unsupervised "cold turkey" approach might be dangerous for problem drinkers or alcoholics.
- **Social Pressure:** I found my friends to be understanding of my habit change. This is not universally true, however, and in some instances it may be necessary to rethink your personal relationships before behavior change can occur.
- **Specific Desires:** Exploration is a strong part of my identity. Others will have different mental cues to tackle or subvert in designing behavior change strategies.
- **Willpower:** If strength and endurance are separable components of the "willpower muscle", it's possible that others may find the endurance of many small decisions easier than the strength of one big decision.

These same factors made elimination an easier form of habit change for me. Although there are general principles of [habit design](http://www.meetup.com/habitdesign/), I believe that further exploration will reveal it to be a *highly personal process.*

{% blockquote %}
It is one thing to say "replace the routine", and an entirely different thing to do so.
{% endblockquote %}

This is not to say that such exploration is hopeless; far from it. If [self-tracking leads to mindfulness](http://quantifiedself.com/2010/12/a-futurists-take-on-self-tracking-and-mindfulness/), perhaps this mindfulness will equip us to *more effectively identify and modify the habit loops that rule our lives.*

## What Next?

My goal is not lifelong abstinence from alcohol. Rather, I'm hoping that this will reset my baseline consumption, making it easier to practice moderation later.

This experience has also demonstrated that elimination is a viable choice for me; if I find that my moderation efforts are slipping, I can return to a period of elimination. Having *proven strategies* under your belt can be enormously helpful in *making behavior change stick.*
