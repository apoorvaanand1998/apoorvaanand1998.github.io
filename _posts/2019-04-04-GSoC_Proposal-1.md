---
layout: post
title: GSoC Proposal - The Student Guide
subtitle: Let's begin 
tags: [Computer Science, Open Source, GSoC, CHAOSS, Proposal]
---

Blogging has always been a good way to organize my thoughts. So, this one, I am starting to help _myself_ write the GSoC Proposal. A part of me is going "Why bother?", I've seen the other candidates, they're honestly quite amazing. I don't stand a chance. But I've gotta try. That's what it's all about, yeah? Enough rambling. 

[This](https://google.github.io/gsocguides/student/finding-the-right-project.html#shortlist) section suggests "to carefully consider what is being proposed, how its scope might be better defined, and how it might fit in with the larger picture"

Here's my attempt at that:

First, here are the [aims](https://github.com/chaoss/grimoirelab/issues/182) of the project (Support of Source Code Related Metrics), from the organization (CHAOSS) itself:
1. Understanding the GrimoireLab components (Perceval, ELK, Mordred and Sigils) and the corresponding tool-chain.
2. Adapting ELK and Mordred to be able to execute Graal and process the data produced.
3. Producing analytics with Graal data and including them in Sigils.
4. Evaluating the implementation with projects of different sizes.
5. Enhancing Graal to support more analysis or improve existing ones are completely within scope.
6. Extending GrimoireLab functionality to integrate Graal.

Let me expand on all of this:
1. [This](https://chaoss.github.io/grimoirelab-tutorial/basics/components.html) page is a good way to understand how the components are organized and how they interact with each other to produce the final analyses/reports.
2. Our project wants to integrate Graal into Grimoirelab so we can view source code metrics in Kibiter. Elk takes the data obtained and converts it into ElasticSearch indices for better search. It also enriches them for more useful metrics. Mordred orchestrates the whole thing by controlling ALL of the grimoirelab components to produce the final dashboard/report. Modify both so they work with Graal seamlessly.
3. Sigils makes the process of making the dashboards in Kibiter super easy. Basically, make Graal work with Sigils. Don't let the users waste too much time building dashboards.
4. After all the integration work is done, make sure the implementation works with backends of all sizes. Lots of problems can occur with a large backend, and that could reveal vulnerabilities/parts of the code that are causing slowdown etc. This needs to be fixed.
5. Graal has many different backends and analyzers. Add to these. For example, use [licensecheck](https://wiki.debian.org/CopyrightReviewTools).
6. All of this can be summed up in the image below:
![Modified Components](/img/modified_components.png) 
(Why link Graal to Arthur? Because Arthur has already been [extended to allow handling of Graal tasks](https://github.com/chaoss/grimoirelab-graal#how-to-integrate-it-with-arthur))

[This](https://google.github.io/gsocguides/student/finding-the-right-project.html#ask-questions) page also tells you to ask questions. Thankfully, [Nishchith](https://github.com/inishchith) has already asked all the right questions. :)

[This](https://google.github.io/gsocguides/student/finding-the-right-project.html#from-project-idea-to-project-plan) part suggests "preparing mock-ups (illustrations, powerpoint, or websites) to help clarify your understanding and vision of the project", hopefully this blog post (and the ones that will come later) will help with that. 
