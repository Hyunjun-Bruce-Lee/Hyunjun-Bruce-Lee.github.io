---
title: Deep Learning
layout: study_main
description: 'Part of a broader family of machine learning methods <br />based on artificial neural networks with representation learning. '
image: assets/images/pic07.jpg
nav-menu: false
show_tile: false
---

<!-- Main -->

<div id="main">
<!-- One -->
<!-- Two -->


{% for post in site.posts %}

{% if post.dl %}

<section id="two" class="spotlights">
	<section class="study_titles">
		<div class="content">
			<div class="inner">
				<header class="major">
					<h3>{{post.title}}</h3>
				</header>
				<p>{{ post.description }}</p>
				<ul class="actions">
					<li><a href="{{ site.baseurl }}{{ post.url }}" class="button">Learn more</a></li>
				</ul>
			</div>
		</div>
        <!--asdasd-->
	</section>
</section>

{% endif %}

{% endfor %}
