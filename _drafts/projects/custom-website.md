---
layout: post
title: Making a Static Website (Affordably!)
# categories: projects
---

## Motivation

This website serves two purposes:

1. **Document Projects**

    I spend a lot of time tinkering with side projects, but documenting these projects is hard. This website will give me a place to store, update, and share notes. 

1. **Satisfy Requirements**

    As a member of the [Engineering Honors Program](https://cuengineeringhonors.com/) at CU Boulder, I need to create and manage an ePortfolio website. 

## Overview

With those goals in mind, I set a few key specifications to guide the process of building my first website:

1. Custom domain name

    I already own the apex domain `cartermak.com`, so I need a host that won't lock me in to a `<cartermak>.<company-name>.com`-type domain.

2. Static Website

    This is less of a requirement and more of a point of guidance. I don't need any databsae functionality and a static website should be cheaper and easier to maintain. 

3. Affordable

    I am a college student, after all. I don't want to pay big fees for my small site. I'm not afraid of tinkering or learning new things, so I steered away from the fancy site-building tools that were out of budget.

These targets guided me to my final solution: a static website, built using [Jekyll](https://jekyllrb.com/) and hosted for free (!!!) using [GitHub Pages](https://pages.github.com/). This struck a balance for me between getting to tinker and learn and needing to build everything from scratch. I've written notes in Markdown for years, but this was my introduction to Ruby and (mostly) HTML. For someone without any coding experience, the process could be a bit daunting, but it's a challenge I was willing to take on.

## Making the Website

*Note: These notes cover the work that I did. This does not constitute a full guide. Visit the Jekyll documentation and read up on Ruby, YML, HTML, and Markdown syntax to get the full picture.*

Perhaps the most overwhelming thing about Jekyll is the sheer number of templates available. I considered building the site content before choosing a template, but because there are slight differences in the naming conventions used by different templates, so I decided against this. 

I checked out a number of different themes by searching for `jekyll-theme` on the [Ruby Gems](https://rubygems.org/search?utf8=%E2%9C%93&query=jekyll-theme) website. One of my favorites was [Hanuman](https://rubygems.org/gems/hanuman), in particular because of its support for Accelerated Mobile Pages (AMP), but it just felt like too many knobs to turn before I could get up and running. In the end, I chose the default theme used b Jekyll when you first create a site: [Minima](https://github.com/jekyll/minima).

### Creating the Initial Site

With this done, the rest of the process was fairly easy. Creating the website begins with installing [Ruby](https://www.ruby-lang.org/en/). Next, I installed the Ruby gems `Jekyll` and `bundler`:

    gem install jekyll bundler

I created a GitHub repository using the necessary naming convention for gh-pages:

    <gh-username>.github.io

Initializing the website is as simple as using one Jekyll command :

    jekyll new <site-name>

This creates a directory called `<site-name>` from which I could build the site, populated with all the necessary files to get started:

<img src="{{ site.baseurl }}/assets/projects/custom-website/jekyll-folder-scructure.png" alt="Default folder contents" align="center" width=200px hspace=25px>

The website is functional in this state! To view it locally, I simply navigate to the new directory and run:

    bundle exec jekyll serve

This starts a local web server on port 4000. I can navigate to it in my web browser using either the loopback IP address: `127.0.0.1:4000`, or the hostname: `localhost:4000`. 

### Making it My Own

All that's left to build the site is to tweak the template to my satisfaction and add content. Here are the small changes I made:

1. Adding social media

    The Minima template makes adding social media to the footer extremely easy. Editing the `_config.yml` file, I only had to remove the included lines and add a few of my own:

    <!-- TODO: figure out why this syntax doesn't work. Will it work when I change the gem from jekyll to gh-pages? -->

    ```diff
    - twitter_username: jekyllrb
    - github_username:  jekyll

    + minima:
    +     social_links:
    +         github: <gh-username>
    +         linkedin: <linkedin-uername>
    ```

    The template handles automatically displaying only the networks for which I provide my information. The full list of supported networks is in the Minima [README](https://github.com/jekyll/minima/blob/master/README.md).

1. Removing the site description from the footer

    I didn't have much to say in my website description, so I removed it from the footer. In order to edit the default layout templates, I first downloaded the full `_includes` folder form the Minima [repository](https://github.com/jekyll/minima) and added the folder to my site's repo. Removing the description from the footer was as simple as removing these lines from `footer.html`:

    ```diff
    - <div class="footer-col one-half">
    -     <p>{{- site.description | escape -}}</p>
    - </div>
    ```

1. Changing the homepage header

    By default, the list of posts on the homepage is titled "Posts". Because this website is supposed to be a project repsitory, I changed this header to "Projects". This change was as simple as adding one key-value pair to the front matter of `index.markdown` (front matter is YML or JSON data written at the top of each markdown file defining relevant parameters; see the example posts):

    ```diff
    + list_title: Projects
    ```
    
    Alternatively, one may copy the `_layouts` folder from the Minima repository and edit the file `home.html` to include any desired changes.

1. Removing the RSS subscription button

    I haven't used RSS feeds for years, and I'm frankly not sure how to anymore, so I removed the button. This required removing a few lines from `home.html`:

    ```diff
    - <p class="feed-subscribe">
    -   <a href="{{ 'feed.xml' | relative_url }}">
    -     <svg class="svg-icon orange"><use xlink:href="{{ 'assets/minima-social-icons.svg#rss' | relative_url }}"></use></svg><span>Subscribe</span>
    -   </a>
    - </p>
    ```

1. Adding a resume

    The Minima template automatically includes all pages (*not* posts) in the header of each page. This seemed like a perfect place to include my resume, so I created a new markdown file, `resume.md`. My current resume is written in LaTeX, so I used [pandoc]() to convert it to markdown, which I then pasted directly onto the page after a little tuning. Easy peasy.

2. Adding misc. Information

    In `_config.yml`, I changed the values of `title`, `email`, and `description` to suit. 

    I also edited `about.markdown` to include some details about myself and the website.

### Adding Content

This is the easiest but most time-consuming part, but for me, it was a great test of my note-taking abilities as I tried to document past projects. The process showed me why having a project repo like this can be so helpful.

## Getting it all online

<!-- Outline -->

- Buying a domain (optional)
- Set domain's A record
- CNAME file
- anything else??? Find the resources I used and read them again...