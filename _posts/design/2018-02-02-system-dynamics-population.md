---
layout: page
sidebar: left
subheadline: System dynamics population model example
title:  "Example System Dynamics Population Model"
teaser: "For beginners to system dynamics modelling and/or Vensim, this is an example model that uses population data from Uganda to show some basic continuous modeling principles."
tags:
    - exploratory modeling
    - policy analysis with python
    - system dynamics
    - population growth
    - article
categories:
    - modeling
header:
   image_fullwidth: "/pop_model2.webp"
show_meta: true
comments: true
---

## Population Growth in Uganda
This is a simple example of modeling population growth in Uganda using system dynamics techniques. System dynamics modeling is beneficial for studying feedback loops, time delays, and other nonlinearities. To create the model, the population is divided into a small number of compartments (e.g. by age). Here, the population is divided into\:
* Infants
* PreSACs (preschool-aged children)
* SACs (school-aged children)
* Adults
* Elderly

<br>
Having a reliable population model is a useful foundation for many public health and policy applications. For instance, I used a version of this population model to estimate the number of Ugandans affected by various gastroenteric pathogens. After projecting those numbers into the future, I could test how different intervention strategies might impact overall morbidity and mortality rates based on this initial population model.

**Related Article**: [Vensim and the Exploratory Modeling Workbench](/vensim-system-dynamics)


![Total number infected]({{site.baseurl}}/images/TLL.webp)

If you are beginner in continuous modeling and/or Vensim, this example may be helpful launching point for your own studies.

[View the full model here](https://github.com/shannongross/code_support/tree/master/vensim_population_model) (Note: Requires [Vensim](https://vensim.com/vensim-software/) to run).


## Other Modeling Posts
{: .t60 }
{% include list-posts tag='modeling' %}
