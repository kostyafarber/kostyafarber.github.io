---
title: My Website
layout: projects
item_colour: "#fccc0a"
item_font: "black"
subtitle: A personal portfolio and other things
description: A website built with Jekyll and GitHub pages that showcases my projects as well as my blog and other writings.
---

I decided to build a website to document my work as well as having a place were I can share my writing about topics I find interesting.

![](../images/iphone-mockup-website.png)
## Plumbing
I used [GitHub pages](https://pages.github.com/) to host the website and a Jekyll [theme](https://jekyllthemes.io/theme/made-portfolio-jekyll-theme) as a base.

## Typography
I love typography and spent a lot of time choosing the right fonts that express my design inclinations.

<div class="grid">
    <div>
        <h1 class="font__grotesk">Founders Grotesk</h1>
    </div>
    <div class="chars__box">
        <h2 class="chars__grotesk" style="color: #ee352e;">abcdefghijklmnopqrstuvwxyz</h2>
        <h2 class="chars__grotesk">ABCDEFGHIJKLMNOPQRSTUVWXYZ</h2>
        <h2 class="chars__grotesk" style="color: #0039a6;">1234567890</h2>
    </div>
    <div class="font__desc">
        <p>
            Founders Grotesk is a beautiful font from the folks at <a href="https://klim.co.nz/">Klim Foundry</a>. 
        </p>
        <p>
            The type is used throughout the site in document headings and as the logo for the footer and header (my name). It's definitely money well spent and looks gorgeous on the web on both mobile and laptop. 
        </p>
        <p>
            A large bold headline really brings out this type and is how I have used it throughout this site.
        </p>
        <p>
            More information on the design can be found <a href="https://klim.co.nz/blog/founders-grotesk-design-information/">here</a> if you are interested.
        </p>
    </div>
    <div>
        <h1 class="font__mono">Berkeley Mono</h1>
    </div>
    <div class="chars__box">
        <h2 class="chars__mono">
        WORLD LEADING PRODUCT INNOVATION Makita® Corporation was founded in 1915 as an electric motor sales and repair company. Today, as a global brand in over 40 countries, Makita
        </h2>
    </div>
    <div class="font__desc">
        <p>
            Berkeley Mono is one of my favorite releases this year. <a href="https://berkeleygraphics.com/">Berkeley Graphics</a> produced the type and their philosophy — Engineering graphics for professionals — really shines. I love everything about Berkeley Graphics, especially their <a href="https://twitter.com/berkeleygfx">Twitter</a>.
        </p>
        <p>
            The title of blog items, projects and the grid on the blog page use Berkeley Mono. It makes for a clean, readable type for content that is usually programming related. Having titles such as: 
            <h2 class="mono__example"><span></span>TIL: bitwise ǀ and & on open flags in UNIX</h2>
        </p>
        <p>
            lend themselves to a crisp display using Berkeley Mono. 
        </p>
        <p>
            I use the type in my IDE and the all code blocks here. It looks clean af.
        </p>
    </div>
    <div class="code__block">
        {% include code_block_website.html %}
    </div>
    <div>
        <h1 class="font__london">London Underground</h1>
    </div>
    <div class="chars__box departures">
        <div class="chars__london">
            <div class="departure__item">
                <div>4</div>
                <div>Bank</div>
                <div class="eta">2 min</div>
            </div>
        </div>
        <div class="chars__london">
            <div class="departure__item">
                <div>3</div>
                <div>Clapham Common</div>
                <div class="eta">3 min</div>
            </div>
        </div>
        <div class="chars__london">
            <div class="departure__item">
                <div>1</div>
                <div>Victora</div>
                <div class="eta">10 min</div>
            </div>
        </div>
    </div>
    <div class="font__desc">
        <p>
            I moved to London in 2022. I catch the tube a lot. Someone dedicated a <a href="https://github.com/petykowski/London-Underground-Dot-Matrix-Typeface">whole project</a> which I found on <a href="https://news.ycombinator.com/item?id=36367667">HN</a> emulating what we see on the LED screen when waiting the short time for the tube to arrive. It's awesome.
        </p>
        <p>
            This is a homage to a new home for me and ends up in a couple of locations on the site. I use it for the dates of my posts and projects as well as the previous and next post text at the end of a blog post.
            <h2 style="font-family: London Underground; font-size: 1rem; color: #ecc12e;">13 DECEMBER 2021 </h2> 
            <h2 style="font-family: London Underground; font-size: 1rem; color: #ecc12e;">24 JULY 2023 </h2> 
        </p>
    </div>
    <div>
        <h1 class="font__mono_tronica">Tronica Mono</h1>
    </div>
    <div class="chars__box">
        <div class="chars__mono_tronica">
            <div class="grep__item">grep(1)</div>
            <div>NAME</div>
            <div class="grep__name">tgrep, egrep, fgrep, rgrep, bzgrep, bzegrep, bzfgrep, zgrep, zegrep, zfgrep – file pattern searched</div>
        </div>
    </div>
    <div class="font__desc">
        <p>
            Tronica Mono is an awesome pixelated terminal like typeface. I love anything pixelated. Tronica makes it's way around the site in a few areas. In the year part of the date in my footer, the numbers that order my projects, small heading on the home page and lastly in the About Me page.
        </p>
    </div>
</div>

## Colours
Most the colours chosen are inspired by various metropolitan subway stations. For instance the New York Subway.

<p align="center">
  <img src="../images/mta-lines.jpeg">
</p>

Of course I have ran out of colours to use from the New York Subway. The tube to the rescue.

<p align="center">
  <img style="border-radius: 10px;" src="../images/tube-stations.webp">
</p>

Eventually I'll have to start using the colours of Skittles or M&Ms.

## Images
I always try to create my own meaningful images that relate to what I am writing about.

![](../images/projects/../gallery/gba-lg.png)

For instance this is a screen grab from a short-lived game based on an awful movie (Toxic Avenger) that is popular with the B-movie crowd.

I used a variation of this in my page about my bad movie project. I made it in Adobe Photoshop using a Nintendo Game Boy Advance mockup.

![](../images/projects/kafka-docker-project/notebook_feature.png)

Another example, for my Bitcoin pipeline project. This features a container (docker) mockup in a notebook, with some awesome marker assets (kafka) I found on Behance. This was also made on Photoshop. I enjoy the process of creating unique graphics to make my posts stand out.

## Inspiration
I find inspiration from unlikely places. Just observing things that I see when I walk around or just getting a general *feel* for what I want to achieve visually works too.

But I couldn't do without these awesome resources:
* [Pinterest](https://www.pinterest.co.uk/)
* [Behance](https://www.behance.net/)
* [Dribble](https://dribbble.com/shots)
* [awwwards](https://www.awwwards.com/)

I think a love of pop culture and culture in general most definitely informs my style and general inclinations towards certain visuals and styles.