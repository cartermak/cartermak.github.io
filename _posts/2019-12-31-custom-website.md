---
layout: post
title: Making a Static Website (Affordably!)
categories: projects
---

# Motivation

This website serves two purposes:

1. **Document Projects**

    I spend a lot of time tinkering with side projects, but documenting these projects is hard. This website will give me a place to store, update, and share notes. 

1. **Satisfy Requirements**

    As a member of the [Engineering Honors Program](https://cuengineeringhonors.com/) at CU Boulder, I need to create and manage an ePortfolio website. 

# Overview

With those goals in mind, I set a few key specifications to guide the process of building my first website:

1. Custom domain name

    I already own the apex domain `cartermak.com`, so I need a host that won't lock me in to a `<cartermak>.<company-name>.com`-type domain.

2. Static Website

    This is less of a requirement and more of a point of guidance. I don't need any databsae functionality and a static website should be cheaper and easier to maintain. 

3. Affordable

    I am a college student, after all. I don't want to pay big fees for my small site. I'm not afraid of tinkering or learning new things, so I steered away from the fancy site-building tools that were out of budget.

These targets guided me to my final solution: a static website, built using [Jekyll](https://jekyllrb.com/) and hosted for free (!!!) using [GitHub Pages](https://pages.github.com/). This struck a balance for me between getting to tinker and learn and needing to build everything from scratch. I've written notes in Markdown for years, but this was my introduction to Ruby and (mostly) HTML. For someone without any coding experience, the process could be a bit daunting, but it's a challenge I was willing to take on.

# Making the Website

*Note: These notes cover the work that I did. This does not constitute a full guide. Visit the Jekyll documentation and read up on Ruby, YML, HTML, and Markdown syntax to get the full picture.*

Perhaps the most overwhelming thing about Jekyll is the sheer number of templates available. I considered building the site content before choosing a template, but because there are slight differences in the naming conventions used by different templates, so I decided against this. 

I checked out a number of different themes by searching for `jekyll-theme` on the [Ruby Gems](https://rubygems.org/search?utf8=%E2%9C%93&query=jekyll-theme) website. One of my favorites was [Hanuman](https://rubygems.org/gems/hanuman), in particular because of its support for Accelerated Mobile Pages (AMP), but it just felt like too many knobs to turn before I could get up and running. In the end, I chose the default theme used b Jekyll when you first create a site: [Minima](https://github.com/jekyll/minima).

## Creating the Initial Site

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

When I want to see what my site looks like on other devices, I can simply add the option `--host 0.0.0.0` to the above command. This "magic IP" tells Jekyll to serve the content to anybody on the local network. From any local device, I can navigate to `<server-IP>:4000` and see my website. 

## Making it My Own

All that's left to build the site is to tweak the template to my satisfaction and add content. Here are the small changes I made:

### Adding social media

The Minima template makes adding social media to the footer extremely easy. Editing the `_config.yml` file, I only had to remove the included lines and add a few of my own:

```diff
- twitter_username: jekyllrb
- github_username:  jekyll
  
+ minima:
+     social_links:
+         github: <gh-username>
+         linkedin: <linkedin-uername>
```

The template handles automatically displaying only the networks for which I provide my information. The full list of supported networks is in the Minima [README](https://github.com/jekyll/minima/blob/master/README.md).

### Removing the site description from the footer

I didn't have much to say in my website description, so I removed it from the footer. In order to edit the default layout templates, I first downloaded the full `_includes` folder form the Minima [repository](https://github.com/jekyll/minima) and added the folder to my site's repo. Removing the description from the footer was as simple as removing these lines from `footer.html`:

```diff
- <div class="footer-col one-half">
-     <p>{{- site.description | escape -}}</p>
- </div>
```

### Changing the homepage header

By default, the list of posts on the homepage is titled "Posts". Because this website is supposed to be a project repsitory, I changed this header to "Projects". This change was as simple as adding one key-value pair to the front matter of `index.markdown` (front matter is YML or JSON data written at the top of each markdown file defining relevant parameters; see the example posts):

```yaml
list_title: Projects
```

Alternatively, one may copy the `_layouts` folder from the Minima repository and edit the file `home.html` to include any desired changes.

### Removing the RSS subscription button

I haven't used RSS feeds for years, and I'm frankly not sure how to anymore, so I removed the button. This required removing a few lines from `home.html`:

```diff
- <p class="feed-subscribe">
-   <a href="{{ 'feed.xml' | relative_url }}">
-     <svg class="svg-icon orange"><use xlink:href="{{ 'assets/minima-social-icons.svg#rss' | relative_url }}"></use></svg><span>Subscribe</span>
-   </a>
- </p>
```

### Removing Post Dates

Minima is a great theme built with blog posts in mind, so everything is referenced by date. I'm happy to sort by date, but I don't need dates displayed everywhere. 

<!-- Outline -->

- Removing dates from posts list on home page
- Removing dates from each post's page (also add a horizontal rule, I think just with `<hr />`???)
- Set default link format as categories/post-name

### Adding a resume

<!-- The Minima template automatically includes all pages (*not* posts) in the header of each page. This seemed like a perfect place to include my resume, so I created a new markdown file, `resume.md`. My current resume is written in LaTeX, so I used [pandoc]() to convert it to markdown, which I then pasted directly onto the page after a little tuning. Easy peasy. -->

The Minima template automatically includes all pages (*not* posts) in the header of each page. This seemed like a perfect place to include my resume, so I created a new markdown file, `resume.md`. My current resume is written in LaTeX, which I compile to a PDF. In the future, I may set up [pandoc](https://pandoc.org/) to convert that LaTeX to markdown, but for the time being, I just insert the full PDF into the page. This uses the users' default browser PDF viewer with a single line in the markdown file (or raw HTML):

```html
<object data="{{ site.baseurl }}/<path-to-file>/resume.pdf" width="100%" height="1100" type='application/pdf'/>
```

### Adding misc. Information

In `_config.yml`, I changed the values of `title`, `email`, and `description` to suit. 

I also edited `about.markdown` to include some details about myself and the website.

## Adding Content

This is the easiest but most time-consuming part, but for me, it was a great test of my note-taking abilities as I tried to document past projects. The process showed me why having a project repo like this can be so helpful.

Jekyll has a great tool for adding content: drafts. Simply create a folder in the site directory called `_drafts` and add markdown files. To preview the drafts, add the `--draft` option to the `jekyll serve` command. 

Once I'm ready to make a post public, I just move the file to the `_posts` folder. In order to be displayed, the file has to follow the naming convention `YYYY-MM-DD-<title>.md`. 

## Adding a Favicon

This is a small detail, but it can make a website look more professional. First, create an icon. I used [favicon.io](https://favicon.io/) to generate a quick icon with my initials on it. I downloaded the `favicon.ico` file and added it to my website's repo. Then, I added one line to the file `head.html`:

```html
<link rel="shortcut icon" href="{{ site.baseurl }}/<path-to-icon>/favicon.ico" />
```
In the future, I might drop into [GIMP](https://www.gimp.org/) and create something a little more sophisticated, but this get's the job done for now.

# Getting it all online

## Using a Custom Domain

I bought my domain through GoDaddy, but the process should be similarly easy anywhere. I also configured using the raw Apex domain; configuring a subdomain (e.g. `www`) is a slightly different process. There are two major steps to complete:

1. Set the custom domain in gh-pages

    In the settings for the site on GitHub, I added my domain to the `Custom domain` field. This added a file to the repository called `CNAME` which identifies my domain name.

1. Configure DNS A record

    For me, this was as simple as adding the GitHub Pages IP addresses to my domain via GoDaddy. I also added a CNAME entry to my DNS record to redirect `www` traffic to my page. 

This [tutorial](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site) from GitHub has a lot more information, including the IP addresses to use. 

## Securing with HTTPS

HTTPS is quickly becoming the standard minimum for website security. Setting up HTTPS is as simple as enabling `Enforce HTTPS` in the gh-pages settings. See [this guide](https://help.github.com/en/github/working-with-github-pages/securing-your-github-pages-site-with-https) for more information.
