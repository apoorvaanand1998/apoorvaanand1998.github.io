---
layout: post
title: GSoC Proposal - Writing the Proposal - 1
subtitle: First Draft
tags: [Computer Science, Open Source, GSoC, CHAOSS, Proposal]
---

For references, I am using the [writing a proposal](https://google.github.io/gsocguides/student/writing-a-proposal) page on the GSoC student guide, as well as the [two example proposals](https://google.github.io/gsocguides/student/proposal-example-1) given at the end. I also managed to find the proposals of the two students who got into CHAOSS last year, which can be found [here](https://docs.google.com/document/d/1VXV_SOazs299KF9_TPRE7FNvJ4ZytkmQYJCT0X4DSgg/edit#heading=h.v80ae7oo7b2c) and [here](https://github.com/kmn5409/chaoss-microtasks/blob/master/GSoC-2018-Keanu-Nichols-CHAOSS-proposal.pdf).

**Title** - Support of Source Code Related Metrics

**Subtitle** - Integrating Graal into the GrimoireLab toolchain

What I intend to convey through the synopsis - I want to focus on integrating graal into the already existing toolchain of GrimoireLab. This means, I want to focus less on expanding Graal's metrics (which I think people with more experience should discuss about), and more on making Graal as valuable and easy to use as Perceval is, to produce dashboards/reports. Of course, this would mean I need to understand how much Graal has already been integrated into the toolchain. I plan on exploring the codebase further (to do this), while writing this proposal and blogging about it here.

**Synopsis** - GrimoireLab produces analytics in the form of dashboards and/or reports. To do this, GrimoireLab uses various tools (such as Perceval, Arthur, GrimoireElk, Sigils, Mordred etc) comprising of a lot of backends (Git, Github, mailing lists, slack, forums etc). The technologies primarily used here are ElasticSearch, for making raw and enriched indices, and Kibana (or Kibiter), for building the dashboards themselves. Graal inherits the Git backend from Perceval and uses third party tools/libraries (such as cloc, nomos, scancode, pylint etc) to produce customizable and incremental source code analysis about code complexity, quality, dependencies, security and licensing. Graal has already been partially integrated into the GrimoireLab toolchain (through [Arthur](https://github.com/chaoss/grimoirelab-graal#how-to-integrate-it-with-arthur)). The goal of this project is to seamlessly integrate Graal into the toolchain, and discuss about/add other kinds of analysis or improve the current ones. 

**Benefits to Community** - One of GrimoireLab's most attractive qualities is how easy it is to use to produce visualizations/analyes/reports. One does not need to know how to use every tool involved in the GrimoireLab ecosystem to make informed decisions through the data visualized/analyses produced. Graal currently does not posses this ease of use. After this project is successfully completed, everyone in the community will be able to leverage the data extracted from source code and use these data in their decision-making processes. As an example, a community will be able to use GrimoireLab to analyze their project, and find out about the package/class dependencies. This can be visualized in the form of a graph in Kibana.

Okay, that's all for this blog post. Next I plan on working on the Plan, Deliverables and the Timeline.
