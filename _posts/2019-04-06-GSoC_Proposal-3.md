---
layout: post
title: Writing the Proposal 2 
subtitle: Exploring the codebase to check the level of integration
tags: [Computer Science, Open Source, GSoC, CHAOSS, Proposal]
---

Here I shall be working on writing on what I believe to be the most important parts of a GSoC proposal - The Plan, the Deliverables and the Timeline. I consider these the hardest to write as well, as these would require me to go through the codebase, check the level of integration of Graal into GrimoireLab and write concise, technical documentation.

The Plan will focus on giving a high level idea of what I am going to do. The Deliverables will list the desired "output" of the project. The Timeline will extrapolate from both the plan and the deliverables, where I shall break down the plan into smaller pieces that explain how I am going to get each deliverable. Deliverables may or may not be labelled as "Required" and "Optional", I shall only be able to know all of this, once I go through the codebase. There's a catch though, as I am going through the codebase, I might discover things that might affect the earlier sections of the proposal, if that happens, I shall be updating them.

Thanks to the microtasks, I've a decent idea about using all the tools in the GrimoireLab toolchain individually, but here I have to explore the lower level approach of all the tools and also how they interact with each other. I shall start by checking out [Arthur](https://github.com/chaoss/grimoirelab-kingarthur) and the [this PR that allows Arthur to handle Graal jobs](https://github.com/chaoss/grimoirelab-kingarthur/pull/33).

Right off the bat, from reading through the Arthur documentation, I've realized that none of the microtasks have made me comfortable with Arthur itself. So, that is the first thing I need to do.

**Possible addition to plan** - Learn how to use Arthur properly - Explore arthur, queue and perform Perceval tasks through Arthur, experiment with executing Graal through Arthur.

Okay, after reading through everything in the Arthur readme page, I've realized that I need to try and use Arthur, at least for simple tasks. I am going to go and create a new virtual environment and test things out. 

- Okay, done installing arthur in a separate venv following the instructions [here](https://github.com/chaoss/grimoirelab-kingarthur#installation). Here's a screenshot:

![Arthur Install](img/arthur_install.png)

Next I will setup the redis and the ElasticSearch server. [Here](https://redis.io/topics/quickstart) are the instructions for redis and the instructions for ElasticSearch can be found on the GrimoireLab tutorial itself.

I've successfully followed the readme at the [Arthur](https://github.com/chaoss/grimoirelab-kingarthur) page and queued/ran Perceval tasks. Here's a screenshot:

![Arthur run](img/arthurw.png)

I noticed that the PR that makes Arthur manage Graal tasks has not been merged into master, so let me make those changes on my local copy of Arthur and see what happens.

[The PR](https://github.com/chaoss/grimoirelab-kingarthur/pull/33) says that "The identification of a graal job is done according to the category name. If it starts with code_, arthur will look for graal backends", this means I need to modify the tasks.json file. 

I have modified the tasks.json file to this:
```
{
    "tasks": [
        {
            "task_id": "arthur.git",
            "backend": "cocom",
            "backend_args": {
                "gitpath": "/tmp/git/arthur.git/",
                "uri": "https://github.com/chaoss/grimoirelab-kingarthur.git",
                "from_date": "2015-03-01"
            },
            "category": "code_commit",
            "scheduler": {
                "delay": 10
		"max_retries": 5
            }
        }
    ]
}
```
Before running Arthur, here are the indices:

![ES indices](img/before.png)
Notice that one of the indices is "items" that we obtained from following the readme in the Arthur page. 

After running arthur, here are the indices:

![ES indices after](img/after.png)
Notice that one of the indices is "graalitems"

I am a bit confused though, docs.count and docs.deleted are 0. Maybe that's how it's supposed to work? Let me look at Elk's code now, to see if running elk creates these indices "properly"

Going through [elk.py](https://github.com/chaoss/grimoirelab-elk/blob/master/grimoire_elk/elk.py#L54), I see that elk takes data to give to Ocean (ElasticSearch) from the Redis queues that are created through Arthur. We see this when we run arthurw (can be seen in a screenshot above). 

**Possible addition to plan** - Learn how to use GrimoireElk properly - Explore GrimoireElk, modify elk.py (feed_backend(), enrich_backend() etc) so that it can create raw and enriched indices from the redis queues created through Arthur. Check kidash (which is a part of Elk) and modify it if necessary so the dashboard defintions work properly. Additionally, the tutorial mentions a p2o.py (Perceval to Ocean) script. Either modify this script to work with Graal or create an analogous g2o.py (Graal to Ocean) script.

This concludes the phase 1 of my plan (which coincides with 1st evaluations). For phase 2, I want to focus on Sigils and understanding how it works alongside with Arthur and Elk.



