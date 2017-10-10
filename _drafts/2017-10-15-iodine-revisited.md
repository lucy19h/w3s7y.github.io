---
layout: post
title:  "DNS tunnels and iodine (Revisited)"
date:   2017-10-15 12:55:00 +0100
categories: blog
---
Introduction
---
So in my older blog "Using DNS tunnels to exfiltrate data and defeat paid for WiFi access points"
I explored using DNS in order to do some pretty nefarious things... However I feel
like I only told half the story (or at least, I had more to say) but the blog was
already over 200 lines long so I thought I'd wrap it up there and leave the other
bits and pieces for another day.  Namely "How would I get the iodine binary into
a closed site that only has DNS lookups in the first place?" and secondly "I'm
not some cracker looking to exfiltrate company secrets from Acme PLC.  Just use
this to get free WiFi!"  In this re-visiting article I will attempt to address
both of these questions.

Using DNS 'TXT' records to infiltrate payloads
---




---
In the previous worked example we gained command line access out of a restricted
network to a network with much less restriction and while it is possible to
perform data exfiltrations and SSH into the network with ease... however, browsing
the internet with a command line browser such as [Lynx](http://lynx.browser.org) isn't
as good as say, using a normal browser.  Therefore let's get all that setup using
docker containers and a bit of port forwarding over the tunnel and a reverse proxy
deployed onto the server-side.  This could then be used by a casual user working
on a restricted network as mentioned in the intro such as an airport or coffee shop.

For this additional piece we will need:
* Docker installed on the client
* [The 'Wormhole'](https://hub.docker.com/benwest/wormhole) container image (yes I'm an MGS fan)
* Nginx installed on the Server and configured as a reverse proxy.

Hopefully the reason as to why we need docker on the client is obvious
(to run the wormhole container).  Nginx can either be installed directly on the
server or, as I do, run docker on the server as well for Nginx (docker fanboy and all!).

What's going to happen is probably best explained with a little picture:

![High Level Design](/assets/img/dtun/hld.jpg)

Premise is quite simple, I will create a centos based docker image which will house
the iodine client and ssh client which will open a SSH connection up to the server
and port forward back to the client.  This port I will then expose and can setup
my browsers proxy config to point to this containers open port as a HTTP proxy.
The SSH connection running over the DNS tunnel will then port forward requests
to the Nginx container running on the iodine server.  Which will then proxy the
HTTP requests out of it's default interface which is internet facing.



Conclusion
---
