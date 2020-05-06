---
layout: default #page
# sidebar: right
title: "Code Tutorials"
meta_title: "Learn something"
subheadline: "Scripts &amp; Code Tips"
teaser: "Example code segments and lessons learned"
permalink: "/code-tutorials/"
header:
   image_fullwidth: "/software.webp" 
---

<div id="blog-index" class="row">
	<div class="small-12 columns t30">
		<h1>{{ snip.title }}</h1>
		{% if snip.teaser %}<p class="teaser">{{ snip.teaser }}</p>{% endif %}

		<dl class="accordion" data-accordion>
			{% assign counter = 1 %}
			{% for snip in site.snips limit:1000 %}
			<dd class="accordion-navigation">
			<a href="#panel{{ counter }}"><span class="iconfont"></span> {% if snip.subheadline %}{{ snip.subheadline }} › {% endif %}<strong>{{ snip.title }}</strong></a>
				<div id="panel{{ counter }}" class="content">
					{% if snip.meta_description %}{{ snip.meta_description | strip_html | escape }}{% elsif snip.teaser %}{{ snip.teaser | strip_html | escape }}{% endif %}
					<a href="{{ site.url }}{{ site.baseurl }}{{ snip.url }}" title="Read {{ snip.title | escape_once }}"><strong>{{ site.data.language.read_more }}</strong></a><br><br>
				</div>
			</dd>
			{% assign counter=counter | plus:1 %}
			{% endfor %}
		</dl>
	</div><!-- /.small-12.columns -->
</div><!-- /.row -->



