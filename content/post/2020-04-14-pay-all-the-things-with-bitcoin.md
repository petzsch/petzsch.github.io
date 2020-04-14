---
title: Pay all the things with Bitcoin
date: 2020-04-14
tags: [bitcoin, btcpayserver, otr, onlinetvrecorder, PHP]
---

As a long time user of [OnlineTvRecorder](https://www.onlinetvrecorder.com) it always bugged me that you couldn't pay them using
my favorite currency (hint hint: Bitcoin). So after I've done several integrations with [BTCPayServer](https://btcpayserver.org/)
it finally was time to change this.

I recently discoverd that you can become a broker for OTR's payment page [we-love-tv.com](https://www.we-love-tv.com) and offer
to accept payments for them. This made my most recent project possible: [we-love-btc.com](https://www.we-love-btc.com/)

How it works:

- The user makes a BTC payment to my site
- after 6 Bitcoin network confirmations (usually takes an hour or so), BTCPayServer sends an Instant Payment Notification (IPN)
  to my server
- that in turn triggers an API call to we-love-tv.com and adds the credits to the users OTR account
- an email get's send to me and the user confirming the transaction

I see this mainly as a proof of concept. But demand is steadly growing.