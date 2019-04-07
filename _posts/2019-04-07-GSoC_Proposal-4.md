---
layout: post
title: Writing the Proposal - 3 
subtitle: Sigils, metrics and Mordred
tags: [Computer Science, Open Source, GSoC, CHAOSS, Proposal]
---

For the phase 2 of my plan (and you guessed it, it coincides with the time period before the second evaluations), I want to understand how [Sigils](https://github.com/chaoss/grimoirelab-sigils) works. In [this](https://github.com/chaoss/grimoirelab-sigils#how-this-info-was-retrieved) section, they mention that the "json files were retrieved taking advantage of the toolchain provided in the grimoirelab project in GitHub. Specifically the script GrimoireELK/utils/kidash.py", what I can gather from this (for now) is that the visualizations are first built and then using kidash, these json files are obtained, that can later be used by Mordred to build dashboards easily. 

**Possible Addition to plan** - Modify Sigils by first modifying the Schema directory for Graal, and then creating new index fields. Extract relevant json by using kidash. Finally, modify Panels so they contain [standard panels](https://github.com/chaoss/grimoirelab-sigils/tree/master/docs#standard-panels) for each of backends in Graal.

I will also be taking part in the discussions involving the addition of other analyzers and backends during the community bonding period. If there are any to be implemented/worked on, those will be implemented using the instructions [here](https://github.com/chaoss/grimoirelab-graal#how-to-develop-a-backend) before working on Sigils. 

This part of the plan is less detail oriented as it involves a bit of discussion, and also my understanding of Sigils is not up to the mark.

The final phase of the plan involves working with Mordred and testing the project. I've chosen to work with Mordred last for two reasons - 
1. It does it's work towards the end in the GrimoireLab toolchain
2. Mordred requires Sigils' Panels to be loaded so it can produce a Kibiter Dashboard

For writing this part of the plan, I shall be looking at [micro-mordred](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/utils/micro.py) which is used to test things during development. 

**Possible addition to plan** - Mofify TaskRawDataCollection class in [task_collection.py](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/sirmordred/task_collection.py#L55) 

**Option deliverable** - Modify [TaskRawDataArthurCollection](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/sirmordred/task_collection.py#L150) along with TaskRawDataCollection.

Honestly, I look at simply the size of that class above, and it scares me. XD

**Possible addition to plan** - Modify [__enrich_items](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/sirmordred/task_enrich.py#L112) so it processes the newly created g2o.py (or modified p2o.py) script's arguments.

**Optional deliverable** - Work on [task_identities.py](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/sirmordred/task_identities.py) if there's time

**Possible addition to plan** - Modify [task_panels.py](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/sirmordred/task_panels.py) so it uses the newly gotten json files from the previous phase of the plan to build dashboards using mordred.

**Possible addition to plan** - Run tests, find spots that cause slowdown, fix them, write documentation.  

I think that's enough investigation for writing the proposal. I am now going to put this all down properly on paper (actually, in a document :P) without all the rambling (hopefully).

