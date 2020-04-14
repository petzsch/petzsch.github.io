---
title: Server moved to Netcup
date: 2019-10-07
tags: [server]
---

After about 1,5 years on a hetzner dedicated server which I was heavily under-utilizing, I finally decided to move all my family related websites and emails to a Netcup KVM server.
This is definitly saving me a buck or two per month and is still more than enough power to run all my services.

I also made the move from Apache to nginx which brought some difficulties with getting Nextcloud to run properly. More on that in a future blog post.

ISPConfig in it's most [recent version](https://www.ispconfig.org/blog/ispconfig-3-1-15-released/) comes with a new SPAM filter (rspamd) which replaces AMAVIS. The results of this
new filter so far are very convincing.

So far I am very happy with Debian 10 bringing PHP 7.3 and all other relevant software in very up2date versions.

I've also ramped up my game when it comes to fighting SPAM. My Domains are now DNSSEC signed, deliver SPF, DKIM and DMARC records.