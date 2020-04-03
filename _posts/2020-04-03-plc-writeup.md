---
layout: post
title: "100% Remote and Autonomous Professional Learning and Development"
video: false
image: prairie.jpg
categories: [learning]
---

I spent the first 10 years of my career teaching (various subjects) and training
teachers. This training work included facilitating PLCs (which I'd say most
public schools have), leading seminars and workshops, and coaching.

Since becoming a software developer, I've had the chance to participate in a lot
of professional development sessions. And since taking my current job with
[Unabridged Software](https://unabridgedsoftware.com) as director of
development, I've been doing a lot of study into how software developers learn.

Software development is somewhat unique in terms of the amount of continued
learning necessary to stay relevant (I spend 15-20 hours per week outside of
work on my own learning, and that's just with things that are immediately
relevant to my work). Software development also has some interesting overlap
with teaching, but that's material for another post.

The biggest problems most teams face is the disjunct between "knowing" and
"doing" -- we know we need to change how we do things, but we haven't done so
yet and may never have the time or chance to do so. Most of my work lately is on
closing that gap.

One technique we've arrived on is professional learning communities, ported over
from my public school days, but with a bit of a twist.

Here is how we do it:

First, our software developers make a list of things they want to learn. Some of
this is out of curiosity, and some if it is out of having problems they don't
currently know how to solve (or where the solution is unsatisfactory). Most of
the time these lists tilt toward solving immediate problems.

In a group I'm working with on my own, a topic we've selected is "Building
mobile applications" (for smartphones). None of us have done that before, though
we have built other types of applications.

Then we divide into groups of 3-5 around topics. The group does a bit of
research and comes up with a guiding question, in the style of *Understanding by
Design*. They also do some conjecturing about what a successful answer might
look like.

In our case, the question became "How do we build a mobile application that
interacts with a Web API?", with a successful answer being (unsurprisingly) a
mobile application that interacts with a Web API. We already know how to build
Web APIs and how to interact with them in other ways, so a mobile application is
a relatively reasonable next step.

From there, we make our best guess (based on research) on the steps we might
need to take: Our guess is something like this:

1. Set up our development environments
2. Build a mobile application that simply displays some static content
3. Modify the application so that responds to user input, e.g. clicking a
   button and changing some static content
4. Modify the application so that it fetches static content from an API
5. Modify the application so it can also send content to the API
6. Figure out authentication (how to handle login/logout and user accounts)
7. Package it into an executable (app) that can be run on both Androids and
   iPhones.

Assuming we can complete these 7 steps, we'll have the ability to start creating
mobile applications for our clients.

But what does this look like in practice?

There are three of us in this particular group, and we have a Web API for which
we're building an integration. We meet weekly, for about 60-90 minutes (over
Zoom, in this case), and we have a shared folder where we keep our code.

We take turns leading meetings. The facilitator for a meeting is responsible
for:

1. Determining with the group if the topic for the week is still appropriate
   (usually it is, but not always)
1. Preparing an exercise to help the group meet the goal for the week
2. Identifying pre-reading and other resources, if any
3. Leading the group through the exercise (and presenting necessary content and
   context)

Thus, we write code together. We look at each other's code (using
screen-sharing). We try variations and experiments with our code. We ask
questions and see if we can figure out the answers. We compare and contrast with
other things we know.

After we're done discussing, two of us write up our notes (paying particular
attention to the metaphors we use and the connections we draw). The notes aren't
usually useful later (that's what the pre-reading is for), but the act of
writing them seems to make the learning last longer (we add meaning to facts, as
Dewey might say).

Then the next week, we do it again.

At the end, we pause and reflect, then decide where to go next.

We typically spend 4-6 weeks on any given topic, and take at least a few weeks
between (we still might meet, but with a much less formal agenda).

Sometimes the big topic is handed down from on-high or dictated by business
needs. Usually it's determined by developers simply knowing what problems
they're facing and imagining what they might do to solve those problems.

Going through this process does help to ease some of the frustration "I know
there's a better way, but we can't do it yet" (and provides a series of
interesting case studies to show to the bosses when trying to justify new
practices). As a bonus, we often get to know each other a little bit better. And
we get to feel like we are doing slightly better work.

We can also go through this process 100% remotely (and have been doing so for
months).

Actually running a PLC Group presents a few more wrinkles than presented here.
If you like, you can [read the full PLC
playbook](https://www.unabridgedsoftware.com/plc-coming-soon/) I wrote for
Unabridged Software and my work there. I'm also happy to talk more with you if
you feel like this is something you want to do in your organization, whether
you're developing software or doing something else. See my [About Page](/about)
for contact information.
