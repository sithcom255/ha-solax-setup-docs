---
title: Preparation
tags:
  - documentation
---

This guide assumes that you already have a device able to run home assistant ( eg.
[Home Assistant Green](https://www.home-assistant.io/green/) or [Raspberry Pi](https://www.raspberrypi.com/)).
I would also suggest you to get a domain name and Cloudflare account.
Otherwise, you just need a bit of time and care :).

### Raspberry Pi

I like the specification of the package
https://rpishop.cz/568453/sada-s-raspberry-pi-5-8gb-ram-pironman-5-250gb-ssd/

You can get the components individually and put it into cheaper case (25% cheaper then the package) and for me this was
quite reasonable. I prefer the 8GB of RAM + 256 GB of SSD to be able to store more historical data directly in HA, and to run Ingress on the side.

You will have to do a bit of exploring since the Pi is available in multiple packages. You can buy the separate board or already with the case. But make sure that
you will be able to fit another extension board (for the SSD) to the case. The Home Assistant can run on the flash card, but it will
crash since the flash is limited to certain number of writes.

The Home Assistant Green is approachable alternative. It offers 4GB of RAM and 32 GB of eMMC (according to the Google, cheaper version of SSD).
If you are not really into building, just get the HA Green.

### Domain Name + Cloudflare

Domain name such as this one (ha-docs.sohai.app) is nice way how to access your HA from outside. It is quite surprising to me that
not many people go through the setup of connecting their smart home to a domain name.

Clouflare is a company providing wide range of services. In this case I am using it to secure my site and monitor incoming attacks.
So if you want to follow you will need a Cloudflare account (Free and you can use your Google account).

I think that many people are just exposing a port on their router and through static ip address are able to connect from their phone.
This works if you have a strong password, but I currently get  ~40 unique visitors per day (so roughly 35 attackers per day), so you probably get some too.

If you decide to implement the part, these are the main advantages:

- Able to view your home from anywhere.
- Security through client certificates or Zero Trust.
- You can use this if you do not have a static IP address, for example when using O2 internet provider.

Just to demonstrate.

- ha.sohai.app is protected with client certificate - you get absolutely nowhere.
- ha-two.sohai.app is protected with Google SSO or Pin Auth by Cloudflare.
### Common shortcuts

HA - Home Assistant
CF - Cloudflare

### Explanations of selected terms
I am quite not sure how far do I need to explain. If you googled something and would like to have it also here, feel free to contact me or submit a PR on github to the docs repo.

- IP - IP address, internet is just like a global post network, everybody has an address. These can change or be dynamic. You will want to have a static address, which means that the we can always find your home under given address
- Port - Your house has a bunch of doors, each designated to different thing. 
