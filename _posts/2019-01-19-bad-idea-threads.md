---
layout: post
title:  "Ousterhout's, Why Threads are a Bad Idea (for most purposes)"
date:   2019-01-19 12:00:00
categories: paper_response
tags: featured
image: /assets/article_images/wizard.jpeg
---

A reminder from John Ousterhout that programming with threads is hard. Event loops, comparatively, are pretty easy. And we can solve a lot of problems with event loops.

This is part of a series of responses I'm writing on classical papers in concurrency--though this is not a paper; it's a talk. I just wanted to revisit it.

#### [Slides](http://web.cecs.pdx.edu/~walpole/class/cs533/papers/ouster.pdf) by John Ousterhout, presented at Sun Microsystem Laboratories. September 28, 1995

## Talk Summary

Basic claim: Compared to concurrency through call-backs, threads are for wizards. (His term.) 

* If only one CPU is available, the event-based model still takes advantage of asynchronous I/O, and using threads to take advantage of asynchronous I/O on a single CPU is kind of a hack.
* In situations where each I/O mechanism has a short-lived handler, events are a simple, reliable solution. For threads, regardless of how short or similarly timed handlers are within an application or system, synchronization requires the same amount of work.
* A multi-threaded model with long-running handlers requires requires careful design to ensure several concurrent, long-running handlers don't leave the application unresponsive.
* On a single CPU, the lack of overhead for TLB misses and lock contention from multi-threading means event-driven code will pretty much always run faster.
* An event-driven application is portable across operating systems and architectures. Threads are basically there now, but in 1995, omg, I can't imagine.

## Relationship to Today

Two huge things have changed in parallel programming since Ousterhout implored us to avoid it. First, we need concurrency. Moore's Law has been creeping to a [halt](https://www.technologyreview.com/s/601441/moores-law-is-dead-now-what/) for the last several years and has relied on multi-core processors for almost two decades to keep going at all. If we want applications to do more, to work faster, or both, we need parallelism. And as Ousterhout points out, fast (non-message-based) parallelism requires threads.

Secondly, user-level thread support has become a thing. Not only do modern OSes provide more asynchronous I/O for a user-level threads scheduler to take advantage of, but OSes provide execution contexts for threads through thread APIs that is much [more efficient](https://en.wikipedia.org/wiki/LinuxThreads) than mapping each one to a process, as was done in Linux until 2002.

I like parallel programming. Sure there aren't tools that work as well for debugging it. There aren't decades of design patterns available. But going forward we will need more parallel solutions than we have wizards. And this shouldn't stop us, because a wizard is a developer who has put in some good practice to make those needed solutions happen.




