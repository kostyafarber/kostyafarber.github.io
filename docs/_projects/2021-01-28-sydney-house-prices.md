---
title: Sydney House Prices
subtitle: Probably what Spider-Man sees when he looks at a map of Sydney.
description: A small project which explores housing prices around Sydney using a Kaggle dataset and various Python libraries.
featured_image: '/sydneyhouseprices/sydneyamazingspiderman.png'
gallery_images:
- /sydneyhouseprices/sydneyamazingspiderman.png
---

## The Process
<br>
As the old adage goes, for pragmatists anyway, you learn by doing. This especially applies to learning programming. 
So I set off into the virtual world to find real world data that wasn't curated to make the coders life easier. 




I first scoured [Kaggle](https://www.kaggle.com/) for data I could use to build an interesting project. My first instinct
was to find data that was close to me in terms of proximity.  




> <img src='../images/projects/sydneyhouseprices/kaggle.png' width=500 />
> 
>Kaggle allows users to find and publish data sets, explore and build models in a web-based data-science environment, work with other data scientists and machine learning engineers, and enter competitions to solve data science challenges.

A simple search of *'Sydney'* into the search bar yielded 
a few results, but being the typical Sydney resident, data of property prices seemed like an obvious option.

## Where I'm At Now
<br>

I have learnt many things whilst working on this small project. What I intend to do is write about the various aspects
and processes I have come across whilst working on this data science project. The list below will include posts about the
many topics covered and my understanding of them.

For example, the post below is a short description of why I started this blog. For now, this [link](https://nbviewer.jupyter.org/github/kostyafarber/sydneyhouseprices/blob/master/notebooks/sydney_choropleth.ipynb) is the jupyter notebook
with the relevant code and concise analyses. Check it out!

<ul class="posts">
{% assign count = 0 %}
{% for post in site.posts %}
  {% if post.tags contains 'sydneyhouseprices' %}
    {% if count < 20 %}
      {% assign count = count|plus:1 %}
      <div class="post_info">
        <li>
          <a href="{{ post.url }}">{{ post.title }}</a>
          <span>({{ post.date | date:"%Y-%m-%d" }})</span>
        </li>
      </div>
    {% endif %}
  {% endif %}
{% endfor %}
</ul>