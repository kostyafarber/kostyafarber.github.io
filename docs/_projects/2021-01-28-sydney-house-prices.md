---
title: Sydney Property Prices Dashboard
layout: projects
subtitle: A Dashboard Built From Scratch
description: A data science project that explores the Sydney property market across different suburbs using a dataset from Kaggle.
featured_image: '/sydneyhouseprices/dashboard.png'
gallery_images:
- /sydneyhouseprices/dashboard.png
project_icons:
    - url: 'https://sydneyhouseprices-dashboard.herokuapp.com/'
      icon_name: 'heroku'
    - url: 'https://github.com/kostyafarber/sydneyhouseprices-dashboard'
      icon_name: 'github'
---

### Links
----
{% include component-project-links.html %}

### Technologies

{% include post-components/gallery.html
	columns = 2
	images = "/images/techstack/matplotlib.svg, /images/techstack/pandas.svg, /images/techstack/heroku.svg, /images/techstack/github.svg, /images/techstack/dash.svg"
%}

### The Motivation

As the old adage goes, for pragmatists anyway, you learn by doing. This especially applies to learning programming. 
So I set off into the virtual world to find real world data that wasn't curated to make the coders life easier. 

I first scoured [Kaggle](https://www.kaggle.com/) for data I could use to build an interesting project. My first instinct
was to find data that was close to me in terms of proximity.  

>Kaggle allows users to find and publish data sets, explore and build models in a web-based data-science environment, work with other data scientists and machine learning engineers, and enter competitions to solve data science challenges.

A simple search of *'Sydney'* into the search bar yielded 
a few results, but being the typical Sydney resident, data of property prices seemed like an obvious option.

### The Result
- A fully custom built interactive dashboard programmed from scratch using **Dash Plotly**, a Python framework for building web analytic applications. 
- The front end application is deployed on **Heroku**, a cloud platform that makes it easy to deploy and manage Flask applications. 
- The data was obtained from Kaggle, a dataset with over 100,000 entries scraped from realestate.com.
- Data wrangling, Exploratory Data Analysis and Data Visualisations were performed using Python and documented in both static and executable (using Binder) Jupyter Notebook for reproducibility.
- All code and project details are open-source and shared on GitHub. 
