---
layout: post
title: "Name Your Patterns"
image: blackberry.jpg
video: false
categories: [technical-debt, communication, software-design]
---

When we jump into a new codebase and begin orienting ourselves, assuming that we
possess the desire to be good teammates and collaborators, there are a few
questions we can ask (these are not the only questions we should ask; merely
some questions we *can* ask):

1. Where does the code live?
2. How is it organized? More specifically, for a given user story, how do I find
   the relevant bits of business logic and system logic?
3. What patterns exist?
4. How do we do things here?
5. Where are the traps?

If I want to add or modify (or remove?) functionality, I need to know where to
find it, how it's written, how it interacts with other functionality, and what
gotchas exist that may make an intuitive solution more challenging.

I also need to know what my team expects in terms of styleguide adherence,
testing, organizing new code, and so on.

To help me (and for me to help others), we need to name these patterns, even if
they are actually antipatterns and even if it makes us feel sad to admit that
our work is less than perfect (or frankly mediocre).

The reason we need to do that is two-fold:

1. By doing so, we can build an accurate mental model of the code
2. We can, piece by piece, begin bending the code in an agreed-upon direction by
   establishing an agreed-upon set of conventions, even if they only apply
   forwards to new code that gets written.

I'll even go so far as to say that it doesn't matter a whole lot what
conventions we agree on for a given codebase, so long as we agree on those
conventions within our team and do our best to follow them.

On my team, we use service objects to encapsulate business logic. Every service
object is named the same way, `Resource::Verb`, e.g. `Dog::Adopt`, and
implements a `perform_using(args)` class method. We write these so that we can
compose them together into complex operations. Sometimes this gets us in trouble
(if, for example, we pick the wrong layer of abstraction), but most of the time
it means that when I am looking at a piece of code, I generally have an idea of
what it's doing, how it's used, and what things depend on it. We do this in lieu
of methods on the model (this is all within the context of Rails).

This is an example of a convention, and one of many we've adopted. We could have
adopted a number of different conventions, but based on the friction points we'd
encountered with the legacy code and our own backgrounds, this is a convention
we settled on. The convention itself is far less important than the deciding.

Now, whenever we bring a new developer on (once every few months thanks to our
rotating internships), we can give them a task and say "Here is how we organize
our codebase, here is the general shape your code should take, and here are some
examples you can look at to see how we organize our code here."

By naming those patterns, we have built-in assumptions for where code might fit,
how it might be written to interact with other code, and where we'll put it. We
have some sense of shared values for evaluating code.

Again, I'm not arguing that the conventions I use are the ones you or anyone
else should use, and in fact the conventions I use are constantly up for
examination and improvement. The important thing here is that we've settled,
through some mixture of experience and experimentation, on patterns that work
well enough for the concerns of the present. Because we have those patterns, I
can lean on those patterns when deciding how to add or extend functionality. I
can explain to other developers where code goes. We can have a shared
conversation about our code, using our jargon and terminology, with some trust
that the way you write code is congruent with the way I write code (and
vice-versa).

And again, that all comes from naming our patterns. We have a lot of legacy code
that doesn't follow our preferred methods of working, but we still name it and
we name how those things work (lots of middleware and non-existent test
coverage, it seems) so we can describe them. There are parts of our patterns
that don't yet work as well as we want, and yet we still name them so we can
discuss them.
