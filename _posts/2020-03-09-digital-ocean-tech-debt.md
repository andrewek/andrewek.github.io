---
layout: post
title: "Commentary: Digital Ocean addresses technical debt"
video: false
image: mousetrap.jpg
categories: [technical-debt, communication, software-design]
---

This writeup by Sunny Beatteay of DigitalOcean, ["From 15,000 database
connections to under 100: DigitalOcean's tale of tech
debt"](https://blog.digitalocean.com/from-15-000-database-connections-to-under-100-digitaloceans-tale-of-tech-debt/)
describes a technical rearchitecture of their stack.

They had been using an *event-sourcing* paradigm, wherein records corresponding
to work to be done were created in a MySQL database and then fetched and
processed by a worker process. In "Gang of Four" design pattern parlance, this
was probably pretty similar to the [Command
pattern](https://en.wikipedia.org/wiki/Command_pattern), in which you represent,
in data, work to be done.

But, like anything, this grew out of control.

> To keep up with the increased Droplet demand, we were adding more and more
> servers to handle the traffic. Each new hypervisor meant another persistent
> connection to the database. By the start of 2016, the database had over 15,000
> direct connections, each one querying for new events every one to five
> seconds. If that was not bad enough, the SQL query that each hypervisor used
> to fetch new Droplet events had also grown in complexity. It had become a
> colossus over 150 lines long and JOINed across 18 tables. It was as impressive
> as it was precarious and difficult to maintain.

So they made changes. The technical changes (using RabbitMQ for an event bus,
restricting direct database access and instead providing an API, etc.) were all
pretty reasonable and predictable. I don't say this as pejorative --
predictability in choices like this often indicates using tools the way they're
meant to be used. I've been in event-sourcing mode for a bit, and the choices
described here are all perfectly sound choices.

The really interesting part here is buried (emphasis mine):

> However, building the interface for the Event queue was the easy part.
> **Getting buy-in from the other teams proved more difficult.** Integrating
> with Harpoon meant teams would have to give up their database access, rewrite
> portions of their codebase, and ultimately change how they had always done
> things. That wasn’t an easy sell.

There are a lot of difficult technical challenges in software. I'll freely
concede this. However, with every single team I've been on (without exception),
the *human* challenges have been greater than the *technical* challenges, even
on teams that worked very well together. And even on teams where there were
significant technical challenges, those challenges were often the result of
crappy processes or choices made a long time ago where there's not sufficient
social/cultural capital to change them. Not always, but often.

This is part of why, when hiring, I look for people who have meaningful
experience beyond writing code, particularly when it comes to navigating the
messiness that is working with other people.

Given that bringing a new developer onto a codebase is almost always asking them
to start from near-scratch (even if they're already familiar with the language
or tools), and given some baseline technical competence, I look for good
communicators and decision-makers when hiring, and do so without regret.

On a team of good communicators, a new member can be brought up to speed, re:
technical needs, relatively quickly. However, on a team of poor communicators
(or even worse, active mis-communicators), even a good developer will founder.

It's rare that a team will sink because of poor technical choices if everything
else is working well. It's often the case that a team will sink because of poor
culture and communication, even if everything else works well.

So we find good communicators and good people, then do our best to help them
succeed. And maybe someday we can do really cool rearchitecture like our
DigitalOcean friends did.
