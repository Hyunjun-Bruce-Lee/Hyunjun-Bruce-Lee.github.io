---
title: Machine Learning
layout: study_main
description: 'Study of computer algorithms <br />that can improve automatically through experience and by the use of data.'
image: assets/images/pic07.jpg
nav-menu: false
show_tile: false
---

<!-- Main -->

<div id="main">
<!-- One -->
<!-- Two -->


{% for post in site.posts %}

{% if post.ml %}

<section id="two" class="spotlights">
	<section class="study_titles">
		<div class="content">
			<div class="inner">
				<a href="{{ site.baseurl }}{{ post.url }}"><header class="major">
					<h3>{{post.title}}</h3> <p>{{ post.description }}</p>
                </header></a>
			</div>
		</div>
	</section>
</section>

{% endif %}

{% endfor %}

