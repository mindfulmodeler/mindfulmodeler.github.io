---
layout: page-fullwidth
breadcrumb: true
format: blog-index
title: "python3"
subheadline: "Scripts &amp; Code Tips"
teaser: "Here are some ideas and features related to Python programming."
header:
   image_fullwidth: "/unsplasB.jpg"
permalink: "/python3/"
widget1:
  title: "Getting Set Up in Python ASAP"
  url: '/snips/easy-peasy-conda-jupyter-setup/'
  image: '/python-conda-setup-title.jpg'
  text: 'A condensed step-by-step guide for installing Python + Anaconda in Windows.'
widget2:
  title: "Advanced Plotting in Seaborn"
  url: '/snips/seaborn-plotting/'
  text: 'Python example for creating overlapping histograms.'
  image: '/hists_title.jpg'
widget3:
  title: "Distribution Fitting with PyStan"
  url: '/snips/distribution-fitting-stan/'
  image: '/pystan_code.jpg'
  text: 'Applying the Stan python package for distribution fitting.'
widget4:
  title: "Automatically convert images to webp format"
  url: '/snips/png-to-webp/'
  image: '/great-nonfiction-books.jpg'
  text: 'A useful powershell script for optimizing entire directories of images into .webp format.'
widget5:
  title: "Rolling Window Function"
  url: '/snips/rolling-window/'
  image: '/lmoments.jpg'
  text: 'An example moving or rolling window function that can be used for statistical smoothing operations.'

---

<div class="row t60">
	{% if page.widget1.image or page.widget1.video or page.widget1.title %}
		{% include _frontpage-widget.html widget=page.widget1 %}
	{% endif %}

	{% if page.widget2.image or page.widget2.video or page.widget2.title %}
		{% include _frontpage-widget.html widget=page.widget2 %}
	{% endif %}

	{% if page.widget3.image or page.widget3.video or page.widget3.title %}
		{% include _frontpage-widget.html widget=page.widget3 %}
    {% endif %}   
</div>

<div class="row t3">
	{% if page.widget4.image or page.widget4.video or page.widget4.title %}
		{% include _frontpage-widget.html widget=page.widget4 %}
    {% endif %}   

	{% if page.widget5.image or page.widget5.video or page.widget5.title %}
		{% include _frontpage-widget.html widget=page.widget5 %}
	{% endif %}

	{% if page.widget6.image or page.widget6.video or page.widget6.title %}
		{% include _frontpage-widget.html widget=page.widget6 %}
    {% endif %}
    
</div>

<!-- 
![exploratory versus predictive modeling]({{site.baseurl}}/images/public-health.jpg)


<div class="row">
   <div class="medium-6 columns">
      {% for post in site.posts limit:1 %}
      {% if post.subheadline %}<p class="subheadline">{{ post.subheadline }}</p>{% endif %}
      <h2><a href="{{ site.url }}{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h2>
      <p>
            {% if post.meta_description %}{{ post.meta_description | strip_html | escape }}{% else post.teaser %}{{ post.teaser | strip_html | escape }}{% endif %}
            <a href="{{ site.url }}{{ site.baseurl }}{{ post.url }}" title="Read {{ post.title | escape_once }}"><strong>{{ site.data.language.read_more }}</strong></a>
      </p>
      {% endfor %}
   </div>

   <div class="medium-6 columns">
      <p><strong>{{ site.data.language.more_articles }}</strong></p>
      {% include list-posts entries='3' offset='1' tag='python' %}
   </div>
</div>

{% include alert success="Yay! you did it!" %}

Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here.

## Ideas and possible new features
{: .t30 } 

* Get rid of Backstretch.js and solve it with pure CSS
* [Custom Scrollbar](https://css-tricks.com/custom-scrollbars-in-webkit/)
* Layout/Template for category-archives -->
 
