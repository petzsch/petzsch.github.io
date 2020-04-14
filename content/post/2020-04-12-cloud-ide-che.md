---
title: Eclipse Che - A Real Cloud IDE on k3s
date: 2020-04-12
---

After comming across an article about Eclipse Che and Theia, I decided to give both a shot. It happens to be that the
[Azure Che Tutorial](https://www.eclipse.org/che/docs/che-7/installing-eclipse-che-on-microsoft-azure/) is quite buggy
and it took me a while to get it running.

For this reason I am writing this little howto on howto get Che running on k3s on any reasonable sized VPS.

## Prequisits

You need a domain on a Cloud DNS Provider that there is a so called "ChallengeProvider" for cert-manager available
for. See this [Link](https://cert-manager.io/docs/configuration/acme/dns01/) for details.

In this howto I will be using the free offer from CloudFlare.

To follow this tutorial you will need a linux command line with root permissions in order to install some tools.
A windows-subsystem for linux environment should also do.

## Choosing a VPS Provider

Generally speaking you want to use a KVM based VPS with AMD64 architecture located near by your geographical location
to avoid latency. What also makes sense to keep in mind is for how long your setup should be running. The great benefit
of cloud providers like AWS or Azure or Hetzner Cloud is that they usually bill you by the hour of usage and that you
can run a test setup for a couple of days easily for under 10 EUR. While getting rather expensive when run for an entire
month.

You will need at least 2 Virtual Private Servers (VPS) to run your cluster on. This is the absolute minimum. One Would
be the k3s master/server and the other the worker/agent. You can expand this setup later on.

As what I'll be using: For the manager I think a [Contabo VPS S SSD](https://contabo.de/?show=vps) should be sufficient
and for the worker it really depends on your expected user count and size of your workspaces. I reckon the
[VPS M SSD](https://contabo.de/?show=vps) from Contabo is generally a good place to start. What stands out here is the
number of CPU cores and the amount of RAM which we need plenty of. In total this setup will cost: 13.98 EUR per month.

## Which OS works for k3s

Generally speaking you can use any modern systemd comptaibile linux that you are comfortable in using. For me that would be
Debian 10 (buster). The makers of k3s [recommend](https://rancher.com/docs/k3s/latest/en/installation/installation-requirements/)
Ubuntu 16.04 or 18.04.

## Installing k3s

### Setting up your master

asdf

### Setting up your agent

asdf

## Installing Che

### Prequisits
