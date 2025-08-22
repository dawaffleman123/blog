---
title: "What is Constellation"
date: 2025-07-15
draft: false
tags:
  - constellation
  - networking
categories:
  - Shit I Did
---


## Genesis

For years when I lived at home, networking was simple, I had the password to the router so all I had to do was log in and port forward something. On top of this I was blessed by my ISP to have a static IP, no CG-NAT drama. This all changed when I went to Purdue for the first year. I very quickly learned that not all places in the world are great for running servers so I was faced with two options. Build my own network, or learn to deal with it.

If you know anything about me, when it comes to networking I will never just “deal with it”. So with the help of some of my friends we built what would later be called Phase 1

## Phase 1

My friends and I were part of the first class of students that did the cybersecurity learning community at Purdue. This meant that from day one they put all of us on the same dorm floor and had events to encourage interaction between the members.

Within the first week we had already taken a trip to the local surplus store and after buying a Dell Poweredge R730, we started building out a fun local network that we could use in my dorm room with goodies such as LanCache for downloading games, various game servers and a pfSense router. This network came from the need to have something that was not the absolutely ass dorm wifi,

Soon just having the network in my dorm was not enough and we needed to expand throughout the hallway. After getting permission from our RA we ran ethernet cables down the hall with switches in certain rooms for easier distribution. At this time we had close to 10 people on the network, with more planning to join.

![Networking Cables on Door](/images/2025/what-is-constellation/cables-door.jpg)

Because cables are a physical thing there is an aspect of physical security that we did not plan for. One day someone cut our cables going down the hallway and we were unable to find out who did it. We did not let this stop us, we re-crimped the cables and got the network set back up.

We thought we had dealt with the biggest issues but we had one issue that we did not think of, rules. We had gotten permission from our RA and it was allowed at Purdue to run the dodgy Chinese string lights down the hallway, however this was not good enough for the maintenance guy who reported us to the building. The head RA then stated that it was a fire hazard to have our unpowered ethernet cables up and forced us to take them down. Not wanting to give up so easily I scheduled an appointment with the fire marshall to try and get permission from them, but quickly found out that almost everything is illegal in the eyes of the fire code.

![String Lights](/images/2025/what-is-constellation/string-lights.jpg)

Not wanting to get expelled from Purdue we took the cables down and started thinking.

## The Tailscale Problem

Tailscale was our next promising solution because we could host it ourselves and just install the client on each device however we quickly ran into an issue. Tailscale works great when every device has a public IP that can open up a port with uPnP. We lived in a dorm so access to good internet was not common. I had access to one public IP that I had gotten from the school but all of our servers existed in other places. Tailscale when it worked was moderately fast but when it did not have a direct connection it was about 3mbps.

After hosting our own Tailscale server with Headscale and DERP server those speeds did not improve much. I tried all kinds of solutions but none of them quite fit what we were trying to make. Until one day my friend m5kro and I were sitting at a pizza place talking about how bad the internet has gotten with brainrot and the other mindless slop on the endless scrolling apps, after seeing a TV in the place playing reels. I said to my friend I bet we could build a better internet and bring it back to the days where true innovation was praised and AI generated slop did not exist.

 > And what do they use to route the internet? BGP.


## Phase 2

I admit there are better ways to set up a network but this was my first time dealing with routing protocols so I chose BGP. Each router that we had would have a 2 bit ASN and a designated range of IPs inside of the 10.72.0.0/14 range. However we needed to choose a router platform because pfSense only had some limited support for BGP. Years ago when looking at what router I should run at my house I came across Vyos but quickly dismissed it because “Who would want a router that doesn’t have a GUI”. I was sorely wrong, because of my cost limitations these routers were some of my best choices for the project we wanted to build. The idea seemed perfect, we only had one issue. We had two weeks to redeploy all of our server infrastructure and networking before winter break

This time was hectic because we had not only classes to deal with but also finals. All of my friends were leaving for the break meaning we either get it all set up before we leave or not have access to our servers for a whole month, meaning not only could we not work on any project we would have to interact with the people at our houses *scary*.

Remember that whole part about needing a public IP for all of this to work? Well I could get one from Purdue but it would take time for that to happen so I set up a server at my house that would bridge the whole network together. So to ping a computer about a mile away the packet would travel about 800 miles. I know, efficient, .

Each one of us would have a wireguard connection to a router that would only route traffic to the 10.72.0.0/14 network. This avoided having to deal with other people’s traffic flowing out our IPs.

## What did we do with this network?

We built smaller services that existed only on the older internet, static HTML sites, FTP servers, and even an Active Directory server we ran on Windows Server. I believe this first real network allowed us to create for the sake of creating without having to worry about networking issues or paying for a cloud server. It was basically throw a wireguard config on there and now you can run anything from anywhere.

The best part was now other people could start creating things too, and through this we inspired other people to start homelabs. This is the true intent of the network.

It may have be small, shitty, and unoptimized but it was a start.

## Why “Phase 2”

A couple years ago I watched the TV show Mr. Robot, a mandatory watch for anyone in Cybersecurity. In the second part of the show Elliot the main character is executing phase 2 of his plan. While I am not trying to cause economic damage I still thought the name was cool.

## Phase 3

After using the network over winter break it became very quickly obvious to us that it needed to be optimized. I started researching OSPF, which was a godsend it how much easier it was to configure. My friend and I both had separate ASNs but we ran OSPF inside of them. Turns out those researchers that made the internet may have known what they were doing.

The major part of phase 3 however were all the projects that ran on top of the network, these are for later articles but the major ones were SSO and DNS.