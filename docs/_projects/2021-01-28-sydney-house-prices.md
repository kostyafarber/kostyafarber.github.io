---
title: Sydney House Prices
layout: projects
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




>Kaggle allows users to find and publish data sets, explore and build models in a web-based data-science environment, work with other data scientists and machine learning engineers, and enter competitions to solve data science challenges.

A simple search of *'Sydney'* into the search bar yielded 
a few results, but being the typical Sydney resident, data of property prices seemed like an obvious option.

## Where I'm At Now
<br>

I have learnt many things whilst working on this small project. I primarily utilise Python libraries **Pandas**, **Seaborn** and **Plotly** to conduct data wrangling, cleaning and visualisation. 
I also adhere to coding good practises and conduct some exploratory data analysis, all presented in the Jupyter notebook link below. What I intend to do is write about the various aspects and processes I have come across whilst working on this data science project. The list below will include posts about the
many topics covered and my understanding of them.

For example, the post below is a short description of why I started this blog. 

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

The relevant project content can be found below:

***Jupyter Notebook***  with the relevant code, graphs and analyses:
- [Sydney House Prices Jupyter notebook](https://nbviewer.jupyter.org/github/kostyafarber/sydneyhouseprices/blob/master/notebooks/sydney_choropleth.ipynb)
  
A dashboard created with the ***Dash***, a productive Python framework for building *web analytic applications*. Written on top of ***Flask, Plotly. js, and React. js***, Dash is ideal for building data visualization apps with highly custom user interfaces in pure Python.
It is deployed on **Heroku** a cloud platform as a service supporting several programming languages
- [Dashboard created with Dash](https://sydneyhouseprices-dashboard.herokuapp.com/) 




