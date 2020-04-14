---
title: Getting Into Kubernetes (K8s)
date: 2020-01-25
tags: [k8s, kubernetes, linux]
---

After working with docker day in and out for almost 2 years, it feels like I've been missing out on the best parts of the whole container ecosystem.

I've signed up for a [cheap managed K8s offer](https://m.do.co/c/767d1bada3e9) with free credits to start with.

They have a great CLI tool - [doctl](https://github.com/digitalocean/doctl) - which you can use to spin up clusters automatically, generate your kubectl config file including oAuth keys and all that good stuff.

After almost giving up because the two big projects I'm intrested in (Jenkins X and GitLab) are not supporting all K8s deployments (mainly just Google and Amazon), I've finally came across the great helm charts repository.

The amount of configuration that goes into a simple nextcloud deployment is very overwhelming. But hey, if you do it, then do it right.

While I haven't given up completly on the utilization of cheap VPS systems from Hetzner or Netcup, I do have to recognize that it all comes down to things like LoadBalancers that you can create from within k8s.

It's been very frustrating failing at the [Kubernetes howto on the hetzner website](https://community.hetzner.com/tutorials/install-kubernetes-cluster) just to find out that the cluster would be missing most critical components. (like said LoadBalancer)