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




> <img src='../images/projects/sydneyhouseprices/kaggle.png' width=500 />
> 
>Kaggle allows users to find and publish data sets, explore and build models in a web-based data-science environment, work with other data scientists and machine learning engineers, and enter competitions to solve data science challenges.

A simple search of *'Sydney'* into the search bar yielded 
a few results, but being the typical Sydney resident, data of property prices seemed like an obvious option.

## Where I'm At Now
<br>

I have learnt many things whilst working on this small project. I primarily utilise Python libraries **Pandas**, **Seaborn** and **Plotly** to conduct data wrangling, cleaning and visualisation. 
I also adhere to coding good practises and conduct some exploratory data analysis, all presented in the Jupyter notebook link below. What I intend to do is write about the various aspects and processes I have come across whilst working on this data science project. The list below will include posts about the
many topics covered and my understanding of them.

For example, the post below is a short description of why I started this blog. For now, this [link](https://nbviewer.jupyter.org/github/kostyafarber/sydneyhouseprices/blob/master/notebooks/sydney_choropleth.ipynb) is the Jupyter notebook
with the relevant code and concise analyses. 

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

Also, check out the code that was the inspiration for this project an interactive choropleth map coded in Plotly showing the median house prices around Sydney.

```python
data = px.choropleth_mapbox(geo_house_prices, 
                            geojson=geo_house_prices.geometry,
                            locations=geo_house_prices.index, color='sellPrice',
                            color_continuous_scale="viridis",
                            center = {"lat": cfg.map.lat, "lon": cfg.map.lon},
                            range_color=(0, 2000000),
                            labels= {"sellPrice":"Selling Price","suburb":"Suburb"},
                            mapbox_style='open-street-map',
                            opacity=0.5
                          )


fig = go.Figure(data = data)


fig.update_layout(margin={"r":0,"t":50,"l":0,"b":0})
fig.update_geos(fitbounds="locations", visible=False)

pyo.plot(fig)
fig.show()
```
<header>

{% include sydneymedian.html %}

</header>

