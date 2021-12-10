---
title: Deep Learning
layout: study_main
description: 'Part of a broader family of machine learning methods <br />based on artificial neural networks with representation learning. '
image: assets/images/pic07.jpg
nav-menu: false
show_tile: false
---



<div>
    &nbsp;<br>&nbsp;
</div>



<div class="row">
{% for post in site.posts %}
{% if post.dl %}
	<div class="4u 12u$(small)">
    <hr class='line_margin'>
        <a href="{{ site.baseurl }}{{ post.url }}"><h2 class='post_order'>{{ post.title }}</h2></a>
        <a href="{{ site.baseurl }}{{ post.url }}"><h5 class='post_order'>{{ post.description }}</h5></a>
	<hr class='line_margin'>
    </div>


{% endif %}
{% endfor %}
</div>

