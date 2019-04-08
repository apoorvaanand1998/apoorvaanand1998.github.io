---
layout: post
title: Modifying the Proposal - 1 
subtitle: Exploring Mordred and Elk's connectors to address feedback
tags: [Computer Science, Open Source, GSoC, CHAOSS, Proposal]
---

For reference, my GSoC proposal (with the comments) is [here](https://docs.google.com/document/d/1il8mNa6lEqHcACR8aaZqf5r-2FpEk6zaB_V9K4A229E/edit?ts=5cab2882).

With the way [@valeriocos](https://github.com/valeriocos) phrased this - "check the list of connectors at: https://github.com/chaoss/grimoirelab-elk/blob/master/grimoire_elk/utils.py#L198, and see how difficult is to a graal backend", it makes me pretty scared to start the investigation from this side, that is, elk -> mordred. I am going to use a bottom-to-top approach here and hopefully that helps.

For understanding mordred, I will be using [micro-mordred] (will be referring to this as "micro")(https://github.com/chaoss/grimoirelab-sirmordred/blob/master/utils/micro.py). First thing I notice - micro needs the setup.cfg and projects.json. setup.cfg contains [Backend Sections](https://github.com/chaoss/grimoirelab-sirmordred#backend-sections) that tells us the name of the backend, the name of the raw and enriched indices and parameters. Projects.json contains the URI of the backend corresponding to a Backend Section in the setup.cfg.

The functions to note in micro are - get_raw() and get_enrich().

get_raw() calls TaskRawDataCollection() and TaskRawDataArthurCollection(), depending on if Arthur is being used.

TaskRawDataCollection() uses [feed_backend()!](https://github.com/chaoss/grimoirelab-sirmordred/blob/53e50547202cb05e22e099192bc6665297488882/sirmordred/task_collection.py#L128) So this path of investigation leads to the connectors as well. I'll stop here for now, and go to get_enrich()

get_enrich() uses the TaskEnrich class in [task_enrich.py](https://github.com/chaoss/grimoirelab-sirmordred/blob/master/sirmordred/task_enrich.py). 

The main function to note in TaskEnrich's __enrich_items is enrich_backend(). Damn! This leads to Elk's connectors too. I guess I _have_ to go investigate things from Elk's side now.

I'm looking at [feed_backend()](https://github.com/chaoss/grimoirelab-elk/blob/master/grimoire_elk/elk.py#L105) and the first thing I notice is that all the parameters of feed_backend() are gotten from the configuration files required for Mordred.

In the first half of the function, the get_connectors() function is used a lot, so if I were to add cocom as a backend section, the get_connectors() function should have an addition of : ` "cocom": [CoCom, CoComOcean, CoComEnrich, CoComCommand]`

[This line](https://github.com/chaoss/grimoirelab-elk/blob/277fb86849421c46ed651e0c4e847e7ad9df00a4/grimoire_elk/elk.py#L136) passes the backend parameters gotten from the config file to connectors[3], which in this case would be CoComCommand.

CoComCommand exists! It inherits from GraalCommand, which in turn inherits from GitCommand! I've used it for one of the microtasks!

My mind is being blown right now. feed_backend() uses a function called [find_signature_paramters()](https://github.com/chaoss/grimoirelab-elk/blob/277fb86849421c46ed651e0c4e847e7ad9df00a4/grimoire_elk/elk.py#L139). This function is imported from perceval, which in turn imports it from the [grimoirelab-toolkit](https://github.com/chaoss/grimoirelab-toolkit/blob/30f36e89f3070f1a7b9973ea3c8a31f4b792ee2b/grimoirelab_toolkit/introspect.py#L62). It does the following :
```
def find_signature_parameters(callable_, candidates,
                              excluded=('self', 'cls')):
    """Find on a set of candidates the parameters needed to execute a callable.
    Returns a dictionary with the `candidates` found on `callable_`.
    When any of the required parameters of a callable is not found,
    it raises a `AttributeError` exception. A signature parameter
    whitout a default value is considered as required.
```
This explains so much. This is such a useful function!

Anyway, so using this function, once it finds the signature candidates in the callable, these candidates are passed to the callable. This is where connector[3], i.e. [backend]Command is used in this process of feed_backend(). What is to be noted is that, Graal backends already have their own [backend]Command, so these need not be implemented. 

Next [we see that](https://github.com/chaoss/grimoirelab-elk/blob/master/grimoire_elk/elk.py#L151) connector[1] is being used, so following through with my earlier example, for cocom it would be - CoComOcean. Does this exist? Let me go check.

For Git, the connector dict has GitOcean and GitEnrich. GitOcean can be found [here](https://github.com/chaoss/grimoirelab-elk/blob/277fb86849421c46ed651e0c4e847e7ad9df00a4/grimoire_elk/raw/git.py#L58). GitOcean inherits from ElasticOcean, which can be found [here.](https://github.com/chaoss/grimoirelab-elk/blob/master/grimoire_elk/raw/elastic.py)

The function to be noted in ElasticOcean is [_items_to_es()](https://github.com/chaoss/grimoirelab-elk/blob/277fb86849421c46ed651e0c4e847e7ad9df00a4/grimoire_elk/raw/elastic.py#L266), which I've already talked about in the comment section of the document! 

Let's look at GitEnrich now. 

OH MY GOD. That class is scary. It has so many LOCs and has so many things going on. But I now understand what I have to do to integrate the Graal backends with Elk!!! :D

