---
title: "Running a 1 MB/s Tor relay on Linode"
date: 2014-06-20
tags:
  - qs
  - technical
layout: layouts/post.njk
---

[Savage Internet](https://savageinter.net/) is proud to announce that we're now running a 1 MB/s [Tor](https://www.torproject.org/) exit relay.  How much is this costing us?  $10/month, thanks to [Linode's](https://www.linode.com/) excellent data transfer caps.  In this post, we'll explain how we set that up.

If you're not sure what Tor is, [read this article](https://www.eff.org/torchallenge/what-is-tor.html).

<!-- more -->

## Our Node

is listed [on Globe](https://globe.torproject.org/#/relay/D85D427500E47F6D1408C883FAB56AF4ED55F3EA).  As of time of writing, we're still [ramping up](https://blog.torproject.org/blog/lifecycle-of-a-new-relay), so our advertised bandwidth will be lower than 1 MB/s for a few days.

## Setting up a Tor Relay on Linode

### Step 1: Set up your Linode instance

Go to [linode.com](https://www.linode.com/), sign up, and add a Linode 1GB instance to your account.  You can follow Linode's [Getting Started instructions](https://library.linode.com/getting-started).  We're using Ubuntu as the distro, mainly because we're familiar with it and we wanted to get this up and running as quickly as possible!

### Step 2: Install Tor

There are some good instructions [here](https://www.darkcoding.net/society/running-a-tor-relay-node-server-on-ubuntu/), but they boil down to:

```bash
$ gpg --keyserver keys.gnupg.net --recv 886DDD89
$ gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | sudo apt-key add -
$ sudo apt-get update
$ sudo apt-get install tor tor-arm
```

Once Tor is installed, you need to configure it.

### Step 3: Basic Tor Configuration

We'll get to exit policies in a bit, but:

- set `ORPort` (or just uncomment it);
- give yourself a `Nickname`, and set `ContactInfo`;
- set `RelayBandwidthRate`, `RelayBandwidthBurst` (in our case, 1 MB/s).

### Step 4: Exit Policy Configuration

The Tor Project recommends [this exit policy](https://trac.torproject.org/projects/tor/wiki/doc/ReducedExitPolicy), which allows roughly 65 ports.

### Step 5: Block BitTorrent using iptables

We went one step further and blocked common markers of BitTorrent traffic, using [this set of iptables rules](https://docs.google.com/document/d/1gaoln96He6yVFcAHoZGPdnDioMrqbABqw2s6nx2wdiI/edit).

### Step 6: Run!

```bash
$ sudo service tor start
$ arm                      # to see awesome graphs
```

## Appendix

### What is Tor?

[EFF's Tor Challenge site](https://www.eff.org/torchallenge/what-is-tor.html) explains that far better than we could:

{% blockquote %}
Tor is a service that helps you to protect your anonymity while using the Internet.
{% endblockquote %}

### Why Linode?

We compared several [virtual private server](https://en.wikipedia.org/wiki/Virtual_private_server) providers.  [Linode](https://www.linode.com/pricing) offers relatively high bandwidth caps: their $10/month plan, for instance, gives you 2TB/month outgoing with unlimited incoming, which is enough to sustain 700 KB/s *24/7*.  [Amazon EC2](https://aws.amazon.com/ec2/) doesn't even compare: bandwidth charges alone for that much traffic would be about $200/month.

[Noisebridge](https://www.noisebridge.net/) runs [four Tor exit relays](https://globe.torproject.org/#/search/query=noiseexit) using QuadraNet dedicated servers. Dedicated servers are more attractive once you ramp up capacity.  With QuadraNet, for instance, $700/month gets you 1Gbps unmetered, or 125 MB/s - Linode 64GB instances are comparable in cost, but those only get you 20TB/month, or 7MB/s. Since our goals are a relatively modest 1 MB/s, this would be overkill; for the same reason, we didn't look into colocation either.

### Why block BitTorrent?  I thought this was about freedom!

From Linode's Terms of Service:

{% blockquote "Linode", "https://www.linode.com/tos", "Linode Terms of Service" %}
Linode does not prohibit the use of distributed, peer to peer network services such as Tor, nor does Linode routinely monitor the network communications of customer Linodes as a normal business practice. However, customers are responsible for the contents of network traffic exiting their Linode. Any usage that prompts the receipt of abuse complaints pertaining to violation of United States and/or international copyright law must be promptly discontinued to avoid service cancellation for violation of these terms.
{% endblockquote %}

In practical terms: if you run an exit relay, Linode *will* receive DMCA takedown notices for your IP address.  They *will* pass those on to you, making them your responsibility.

To mitigate this risk, we block BitTorrent.  Otherwise we'll eventually have to

- take down the node; or
- `ExitPolicy reject *:*`; or
- move elsewhere.

An offline node is of use to no one.  A middle relay is less useful, since overall Tor network performance relies upon having exit nodes.  Moving elsewhere is doable, but it would definitely be less cost-effective (at least at our current scale - see below).

Another option is to donate to other relay operators.  Donations are more cost-effective in increasing Tor network bandwidth, but this comes [at the expense of network diversity](https://blog.torproject.org/blog/turning-funding-more-exit-relays).  (If you don't see why this is a problem, consider what happens when a malicious actor - NSA/GCHQ/etc., for instance - operates some proportion of Tor relays.)

Even if Linode handled DMCA complaints differently, a relay that's swamped with high-bandwidth, high-connection-count traffic from BitTorrent is of use to far fewer people than one that isn't.  We'd rather support people who *need* Tor than some dude who just can't find that awesome movie on Netflix.

If that's not enough for you, the Tor Project itself notes that [BitTorrent over Tor isn't a good idea](https://blog.torproject.org/blog/bittorrent-over-tor-isnt-good-idea), as it leaks identifying information and generally hurts network performance.

So: we have nothing against BitTorrent, and we do wish the DMCA would burn and die, but we will make every effort possible to prevent BitTorrent traffic from running through our relay.

### Last Words

This is easy to do and relatively inexpensive, and if you run a 1 MB/s relay you [might get a T-shirt from the EFF](https://www.eff.org/torchallenge/#getstarted).
