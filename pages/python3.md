---
layout: page
format: blog-index
title: "python3"
subheadline: "Scripts &amp; Code Tips"
teaser: "Here are some ideas and features related to Python programming."
header:
   image_fullwidth: "/header_roadmap_3.jpg"
permalink: "/python3/"

widget1:
  title: "Moving Window Tutorial"
  url: '/tutorial/'
  image: '/modeling/NTD-system-dynamics/'
  text: 'Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. '
widget2:
  title: "Django Foreign Key Mapping"
  url: '/tutorial/'
  text: 'Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. '
  image: '/modeling/NTD-system-dynamics/'
widget3:
  title: "Calculating L-Moments"
  url: '/tutorial/'
  image: '/modeling/NTD-system-dynamics/'
  text: 'Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. '
---
## heya
Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here. Random paragraph here.


![exploratory versus predictive modeling]({{site.baseurl}}/images/public-health.webp)


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
* Layout/Template for category-archives
 
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