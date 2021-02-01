---
title: What Questionable Movies Share
subtitle: What do bad movies share? An inquiry into the spirit of bad things.
description: An analysis of a list me and my friends have compiled over the years whilst watching films that we considered so bad they were good. Suffice to say, not all of them where as funny as we thought. I decided to dig deeper and extract relationships and insights from these films.
featured_image: '/trash_movies/cinema.jpg'
gallery_images:
- /trash_movies/trashmovies.jpg
---

# How It All Starts
<br>
One of my fond memories of a bygone era was visiting the local video store, the now ancient ***Video Ezy***, to pick up a movie with my friends. We would go
to each others houses and have a movie marathon and watch all types of films. Some good, some bad. 

![](../images/projects/trash_movies/videoezy.jpg)

Over the years we all naturally became avid *cinephiles*. Analysing films while watching them became a favourite pastime and
surprisingly, the bad films had plenty of (hilarious) things to analyse. What followed was uncovering a giant underground cult following of all things
bad. 

One particularly brilliant medium that explored this sub-genre of movie, was the podcast *How Did This Get Made*. 

> How Did This Get Made? is a podcast on the Earwolf network. It is hosted by Paul Scheer, June Diane Raphael and Jason Mantzoukas. Each episode, which typically has a different guest, features the deconstruction and mockery of outlandish and bad films.

After listening to this podcast religiously, me and my friends decided, why not create our own corpus of bad movies. So the bad
movie club is born, and 200+ movies later a rather interesting (to me at least) dataset is produced.

I've always had the idea to create a data science project from our long and silly list, so here it is. It is currently a work in progress. As I progress
further with whatever comes out of this, the relevant posts will appear below in a list, kind of like this one:

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

For now, you can check out this [link](https://github.com/kostyafarber/trash-movie-classifier) for the GitHub repository to see what im up to.

Hopefully by the end of this I will be able to answer the question: 

### What Do Bad Movies Share?